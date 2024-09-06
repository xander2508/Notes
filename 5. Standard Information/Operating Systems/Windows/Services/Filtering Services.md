---
tags:
  - OperatingSystems
  - Windows
  - Services
  - StandardInformation
---


```powershell-session
Get-Service | where DisplayName -like '*Defender*'
```