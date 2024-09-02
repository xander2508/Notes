---
tags:
  - OperatingSystems
  - Windows
  - PowerShell
---

[about Execution Policies - PowerShell | Microsoft Learn](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2)

As outlined in Microsoft's official documentation, an execution policy is not a security control. It is designed to give IT admins a tool to set parameters and safeguards for themselves.

```powershell-session
Get-ExecutionPolicy 
```

```powershell-session
Set-ExecutionPolicy undefined 
```

By changing it at the Process level, our change will revert once we close the PowerShell session. Keep the execution policy in mind when working with scripts and new modules.

```powershell-session
Set-ExecutionPolicy -scope Process 
```
