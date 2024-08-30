---
tags:
  - OperatingSystems
  - Windows
  - Tooling
---
 [WMIC](https://ss64.com/nt/wmic.html)

The Windows Management Instrumentation Command (`WMIC`) allows us to retrieve a vast range of information from our local host or host(s) across the network. The versatility of this command is wide in that it allows for pulling such a wide arrangement of information.


# List Services 

```cmd-session
wmic service list brief
```