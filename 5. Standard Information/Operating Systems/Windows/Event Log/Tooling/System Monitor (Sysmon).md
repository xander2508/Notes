---
tags:
  - OperatingSystems
  - Windows
  - EventLog
  - Tooling
  - StandardInformation
---
To enhance our event log coverage, we can extend the capabilities by incorporating Sysmon, which offers additional event logging capabilities.


`System Monitor (Sysmon)` is a Windows system service and device driver that remains resident across system reboots to monitor and log system activity to the Windows event log. Sysmon provides detailed information about process creation, network connections, changes to file creation time, and more.

Sysmon's primary components include:

- A Windows service for monitoring system activity.
- A device driver that assists in capturing the system activity data.
- An event log to display captured activity data.

The full list of Sysmon event IDs can be found [here](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon).

To view these events, navigate to the Event Viewer and access "Applications and Services" -> "Microsoft" -> "Windows" -> "Sysmon."
# Configuration

For customisation and granular control, Sysmon uses an XML configuration file:

- For a comprehensive configuration, we can visit: [https://github.com/SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config).
- Another option is: [https://github.com/olafhartong/sysmon-modular](https://github.com/olafhartong/sysmon-modular), which provides a modular approach.

# Install

To get started, you can install Sysmon by downloading it from the official Microsoft documentation ([https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)). Once downloaded, open an administrator command prompt and execute the following command to install Sysmon.

```shell-session
sysmon.exe -i -accepteula -h md5,sha256,imphash -l -n
```

To utilize a custom Sysmon configuration, execute the following after installing Sysmon.

```shell-session
sysmon.exe -c filename.xml
```

# Detection Example 1: Detecting DLL Hijacking

To detect a DLL hijack, we need to focus on `Event Type 7`, which corresponds to module load events. To achieve this, we need to modify the `sysmonconfig-export.xml`.
## Modifying Configuration

By examining the modified configuration, we can observe that the "include" comment signifies events that should be included.

![[image14.webp]]

In the case of detecting DLL hijacks, we change the "include" to "exclude" to ensure that nothing is excluded, allowing us to capture the necessary data.

![[image15.webp]]

To utilize the updated Sysmon configuration, execute the following.

```shell-session
sysmon.exe -c sysmonconfig-export.xml
```

To view these events, navigate to the Event Viewer and access "Applications and Services" -> "Microsoft" -> "Windows" -> "Sysmon."

## DLL Attack

Let's attempt the hijack using "calc.exe" and "WININET.dll" as an example. To simplify the process, we can utilize Stephen Fewer's "hello world" [reflective DLL](https://github.com/stephenfewer/ReflectiveDLLInjection/tree/master/bin). It should be noted that DLL hijacking does not require reflective DLLs.

By following the required steps, which involve renaming `reflective_dll.x64.dll` to `WININET.dll`, moving `calc.exe` from `C:\Windows\System32` along with `WININET.dll` to a writable directory (such as the `Desktop` folder), and executing `calc.exe`, we achieve success. Instead of the Calculator application, a [MessageBox](https://learn.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-messageboxa) is displayed.

Next, we analyse the impact of the hijack. First, we filter the event logs to focus on `Event ID 7`, which represents module load events, by clicking "Filter Current Log...".

![[image21 1.webp]]

Subsequently, we search for instances of "calc.exe", by clicking "Find...", to identify the DLL load associated with our hijack.

Let's explore these indicators of compromise (IOC):

1. "calc.exe", originally located in System32, should not be found in a writable directory. Therefore, a copy of "calc.exe" in a writable directory serves as an IOC, as it should always reside in System32 or potentially Syswow64.
2. "WININET.dll", originally located in System32, should not be loaded outside of System32 by calc.exe. If instances of "WININET.dll" loading occur outside of System32 with "calc.exe" as the parent process, it indicates a DLL hijack within calc.exe.
3. The original "WININET.dll" is Microsoft-signed, while our injected DLL remains unsigned.

# Detection Example 2: Detecting Unmanaged PowerShell/C-Sharp Injection

C# is considered a "managed" language, meaning it requires a backend runtime to execute its code. The [Common Language Runtime (CLR)](https://docs.microsoft.com/en-us/dotnet/standard/clr) serves as this runtime environment. [Managed code](https://docs.microsoft.com/en-us/dotnet/standard/managed-code) does not directly run as assembly; instead, it is compiled into a bytecode format that the runtime processes and executes. Consequently, a managed process relies on the CLR to execute C# code.

As defenders, we can leverage this knowledge to detect unusual C# injections or executions within our environment. To accomplish this, we can utilize a useful utility called [Process Hacker](https://processhacker.sourceforge.io/).

Within Process Hacker, examining the module loads for `powershell.exe`, by right-clicking on `powershell.exe`, clicking "Properties", and navigating to "Modules", we can find relevant information.

The presence of "Microsoft .NET Runtime...", `clr.dll`, and `clrjit.dll` should attract our attention. These 2 DLLs are used when C# code is ran as part of the runtime to execute the bytecode. If we observe these DLLs loaded in processes that typically do not require them, it suggests a potential [execute-assembly](https://www.cobaltstrike.com/blog/cobalt-strike-3-11-the-snake-that-eats-its-tail/) or [unmanaged PowerShell injection](https://www.youtube.com/watch?v=7tvfb9poTKg&ab_channel=RaphaelMudge) attack.

To showcase unmanaged PowerShell injection, we can inject an [unmanaged PowerShell-like DLL](https://github.com/leechristensen/UnmanagedPowerShell) into a random process, such as `spoolsv.exe`. We can do that by utilizing the [PSInject project](https://github.com/EmpireProject/PSInject) in the following manner.

```powershell-session
 powershell -ep bypass
 Import-Module .\Invoke-PSInject.ps1
 Invoke-PSInject -ProcId [Process ID of spoolsv.exe] -PoshCode "V3JpdGUtSG9zdCAiSGVsbG8sIEd1cnU5OSEi"
```

After the injection, we observe that "spoolsv.exe" transitions from an unmanaged to a managed state as it is running Powershell.exe.

# Detection Example 3: Detecting Credential Dumping

One widely used tool for credential dumping is [Mimikatz](https://github.com/gentilkiwi/mimikatz), offering various methods for extracting Windows credentials. One specific command, "sekurlsa::logonpasswords", enables the dumping of password hashes or plaintext passwords by accessing the [Local Security Authority Subsystem Service (LSASS)](https://en.wikipedia.org/wiki/Local_Security_Authority_Subsystem_Service). LSASS is responsible for managing user credentials and is a primary target for credential-dumping tools like Mimikatz.

```cmd-session
C:\Tools\Mimikatz> mimikatz.exe

  .#####.   mimikatz 2.2.0 (x64) #18362 Feb 29 2020 11:13:36
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > http://blog.gentilkiwi.com/mimikatz
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )
  '#####'        > http://pingcastle.com / http://mysmartlogon.com   ***/

mimikatz # privilege::debug
Privilege '20' OK

mimikatz # sekurlsa::logonpasswords

Authentication Id : 0 ; 1128191 (00000000:001136ff)
Session           : RemoteInteractive from 2
User Name         : Administrator
Domain            : DESKTOP-NU10MTO
Logon Server      : DESKTOP-NU10MTO
Logon Time        : 5/31/2023 4:14:41 PM
SID               : S-1-5-21-2712802632-2324259492-1677155984-500
        msv :
         [00000003] Primary
         * Username : Administrator
         * Domain   : DESKTOP-NU10MTO
         * NTLM     : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
         * SHA1     : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX0812156b
        tspkg :
        wdigest :
         * Username : Administrator
         * Domain   : DESKTOP-NU10MTO
         * Password : (null)
        kerberos :
         * Username : Administrator
         * Domain   : DESKTOP-NU10MTO
         * Password : (null)
        ssp :   KO
        credman :
```

As we can see, the output of the "sekurlsa::logonpasswords" command provides powerful insights into compromised credentials.

To detect this activity, we can rely on a different Sysmon event. Instead of focusing on DLL loads, we shift our attention to process access events. By checking `Sysmon event ID 10`, which represents "ProcessAccess" events, we can identify any suspicious attempts to access LSASS.

![[image33.webp]]

Please note that some legitimate processes may access LSASS, such as authentication-related processes or security tools like AV or EDR.