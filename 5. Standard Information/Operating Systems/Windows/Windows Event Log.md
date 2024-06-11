An `event` is any action or occurrence that can be identified and classified by a system's hardware or software.

`Events` can be generated or triggered through a variety of different ways including some of the following:
- User-Generated Events
    - Movement of a mouse, typing on a keyboard, other user-controlled peripherals, etc.
- Application Generated Events
    - Application updates, crashes, memory usage/consumption, etc.
- System Generated Events
    - System uptime, system updates, driver loading/unloading, user login, etc.

 The `Event Log` manages events and event logs, however, in addition to this functionality it also opens up a special API that allows applications to maintain and manage their own separate logs.

## Event Log Categories and Types

|Log Category|Log Description|
|---|---|
|System Log|The system log contains events related to the Windows system and its components. A system-level event could be a service failing at startup.|
|Security Log|Self-explanatory; these include security-related events such as failed and successful logins, and file creation/deletion. These can be used to detect various types of attacks that we will cover in later modules.|
|Application Log|This stores events related to any software/application installed on the system. For example, if Slack has trouble starting it will be recorded in this log.|
|Setup Log|This log holds any events that are generated when the Windows operating system is installed. In a domain environment, events related to Active Directory will be recorded in this log on domain controller hosts.|
|Forwarded Events|Logs that are forwarded from other hosts within the same network.|
## Event Types

|Type of Event|Event Description|
|---|---|
|Error|Indicates a major problem, such as a service failing to load during startup, has occurred.|
|Warning|A less significant log but one that may indicate a possible problem in the future. One example is low disk space. A Warning event will be logged to note that a problem may occur down the road. A Warning event is typically when an application can recover from the event without losing functionality or data.|
|Information|Recorded upon the successful operation of an application, driver, or service, such as when a network driver loads successfully. Typically not every desktop application will log an event each time they start, as this could lead to a considerable amount of extra "noise" in the logs.|
|Success Audit|Recorded when an audited security access attempt is successful, such as when a user logs on to a system.|
|Failure Audit|Recorded when an audited security access attempt fails, such as when a user attempts to log in but types their password in wrong. Many audit failure events could indicate an attack, such as Password Spraying.|
## Event Severity Levels

|Severity Level|Level #|Description|
|---|---|---|
|Verbose|5|Progress or success messages.|
|Information|4|An event that occurred on the system but did not cause any issues.|
|Warning|3|A potential problem that a sysadmin should dig into.|
|Error|2|An issue related to the system or service that does not require immediate attention.|
|Critical|1|This indicates a significant issue related to an application or a system that requires urgent attention by a sysadmin that, if not addressed, could lead to system or application instability.|

## Elements of a Windows Event Log

- `Log name`: As discussed above, the name of the event log where the events will be written. By default, events are logged for `system`, `security`, and `applications`.
- `Event date/time`: Date and time when the event occurred
- `Task Category`: The type of recorded event log
- `Event ID`: A unique identifier for sysadmins to identify a specific logged event
- `Source`: Where the log originated from, typically the name of a program or software application
- `Level`: Severity level of the event. This can be information, error, verbose, warning, critical
- `User`: Username of who logged onto the host when the event occurred
- `Computer`: Name of the computer where the event is logged
- 
There are many Event IDs that an organization can monitor to detect various issues. In an Active Directory environment, [this list](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/appendix-l--events-to-monitor) includes key events that are recommended to be monitored for to look for signs of a compromise. 
[This](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/) searchable database of Event IDs is worth perusing to understand the depth of logging possible on a Windows system.

## Windows Event Log Technical Details

The Windows Event Log is handled by the `EventLog` services. On a Windows system, the service's display name is `Windows Event Log`, and it runs inside the service host process [svchost.exe](https://en.wikipedia.org/wiki/Svchost.exe). It is set to start automatically at system boot by default.

By default, Windows Event Logs are stored in `C:\Windows\System32\winevt\logs` with the file extension `.evtx`.

## Interacting with the Windows Event Log

### wevtutil

The [wevtutil](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil) command line utility can be used to retrieve information about event logs. It can also be used to export, archive, and clear logs, among other commands.

#### Enumerating Log Sources

```cmd-session
wevtutil el
```

#### Gathering Log Information

With the `gl` parameter, we can display configuration information for a specific log, notably whether the log is enabled or not, the maximum size, permissions, and where the log is stored on the system.

```cmd-session
wevtutil gl "Windows PowerShell"
```

The `gli` parameter will give us specific status information about the log or log file, such as the creation time, last access and write times, file size, number of log records, and more.

```cmd-session
 wevtutil gli "Windows PowerShell"
```

#### Querying Events

For example, let's say we want to display the last 5 most recent events from the Security log in text format.
Local admin access is needed for this command.

```cmd-session
wevtutil qe Security /c:5 /rd:true /f:text
```

#### Exporting Events

```cmd-session
wevtutil epl System C:\system_export.evtx
```

### PowerShell

#### PowerShell - Listing All Logs

```powershell-session
Get-WinEvent -ListLog *
```

#### Security Log Details

```powershell-session
Get-WinEvent -ListLog Security
```

#### Querying Last Five Events

Here we will list the last five events recorded in the Security log. By default, the newest logs are listed first. If we want to get older logs first, we can reverse the order to list the oldest ones first using the `-Oldest` parameter.

We can query for the last X number of events, looking specifically for the last five events using the `-MaxEvents` parameter.

```powershell-session
Get-WinEvent -LogName 'Security' -MaxEvents 5 | Select-Object -ExpandProperty Message
```

From here, we could use the `-ExpandProperty` parameter to dig deeper into specific events, list logs from oldest to newest, etc.

#### Filtering for Logon Failures

```powershell-session
Get-WinEvent -FilterHashTable @{LogName='Security';ID='4625 '}
```

```powershell-session
Get-WinEvent -FilterHashTable @{LogName='System';Level='1'} | select-object -ExpandProperty Message
```


#### Guides 

Microsoft provides some [examples](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-7.3) for `Get-WinEvent`, while [this site](https://www.thewindowsclub.com/what-is-wevtutil-and-how-do-you-use-it) shows examples for `wevtutil`, and [this site](https://4sysops.com/archives/search-the-event-log-with-the-get-winevent-powershell-cmdlet/) has some additional examples for using `Get-WinEvent`.