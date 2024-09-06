---
tags:
  - OperatingSystems
  - Windows
  - Services
  - StandardInformation
---
[Tasklist](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist) is a command line tool that gives us a list of currently running processes on a local or remote host. However, we can utilize the `/svc` parameter to provide a list of services running under each process on the system.

```
tasklist /SVC
```