---
tags:
  - OperatingSystems
  - Windows
  - Services
---


```powershell-session
Get-Service | where DisplayName -like '*Defender*'
```