Use the GUI and XML filtering if possible

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
