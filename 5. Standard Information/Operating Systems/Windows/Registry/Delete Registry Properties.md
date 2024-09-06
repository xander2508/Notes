---
tags:
  - OperatingSystems
  - Windows
  - Registry
  - StandardInformation
---
Removing entries from the Windows Registry could negatively affect the host and how it functions. Be sure you know what it is you are removing before.

```powershell-session
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\TestKey -Name  "access"
```