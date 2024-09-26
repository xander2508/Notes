---
tags:
  - Enumeration
  - TCP
  - MSSQL
  - Concepts
  - Information
---
By default, `MSSQL` allows file read on any file in the operating system to which the account has read access. We can use the following SQL query:

```cmd-session
SELECT * FROM OPENROWSET(BULK N'C:/Windows/System32/drivers/etc/hosts', SINGLE_CLOB) AS Contents
```

