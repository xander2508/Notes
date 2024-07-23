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

## Detection Example 1: Detecting DLL Hijacking

To detect a DLL hijack, we need to focus on `Event Type 7`, which corresponds to module load events. To achieve this, we need to modify the `sysmonconfig-export.xml`.
 
By examining the modified configuration, we can observe that the "include" comment signifies events that should be included.

![[image14.webp]]

In the case of detecting DLL hijacks, we change the "include" to "exclude" to ensure that nothing is excluded, allowing us to capture the necessary data.

![[image15.webp]]

To utilize the updated Sysmon configuration, execute the following.

```shell-session
sysmon.exe -c sysmonconfig-export.xml
```

To view these events, navigate to the Event Viewer and access "Applications and Services" -> "Microsoft" -> "Windows" -> "Sysmon."