---
tags:
  - Enumeration
  - TCP
  - MySQL
  - SQL
  - Tooling
---
The **sqlcmd** utility is a command-line utility for ad hoc, interactive execution of Transact-SQL (T-SQL) statements and scripts and for automating T-SQL scripting tasks.

[sqlcmd - Use the sqlcmd utility - SQL Server | Microsoft Learn](https://learn.microsoft.com/en-us/sql/tools/sqlcmd/sqlcmd-use-utility?view=sql-server-ver16)
## Usage

```cmd-session
sqlcmd -S 10.129.20.13 -U username -P Password123
```

```cmd-session
sqlcmd -S SRVMSSQL -U julio -P 'MyPassword!' -y 30 -Y 30
```

> [!NOTE]
> When we authenticate to MSSQL using `sqlcmd` we can use the parameters `-y` (SQLCMDMAXVARTYPEWIDTH) and `-Y` (SQLCMDMAXFIXEDTYPEWIDTH) for better looking output. Keep in mind it may affect performance.

If we use `sqlcmd`, we will need to use `GO` after our query to execute the SQL syntax.

```cmd-session
1> SELECT name FROM master.dbo.sysdatabases
2> GO
```