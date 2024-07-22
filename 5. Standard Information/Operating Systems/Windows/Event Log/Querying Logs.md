To streamline our analysis, we can create custom XML queries to identify related events using the "Logon ID" as a starting point. 

By navigating to "Filter Current Log" -> "XML" -> "Edit Query Manually," we gain access to a custom XML query language that enables more granular log searches.

![[image7.webp]]

It is worth noting that if assistance is required in crafting the query, automatic filters can be enabled, allowing exploration of their impact on the XML representation. For further guidance, Microsoft offers informative articles on [advanced XML filtering in the Windows Event Viewer](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/advanced-xml-filtering-in-the-windows-event-viewer/ba-p/399761).

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

```
$time1 =  get-date('08/03/2022 10:23:24')
```
```
$time2 =  get-date('08/03/2022 10:23:26')```
```
```
Get-WinEvent -FilterHashtable @{LogName = 'Security'; Id = 4624; StartTime = $time1; EndTime = $time2 } 
```
