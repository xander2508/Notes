# Managing Domain Users and Groups

`ActiveDirectory` PowerShell Module is required to manage users and groups with PowerShell. Another requirement is to have the optional feature `Remote System Administration Tools` installed

```powershell-session
Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability -Online
```

Ensure the PowerShell Active Directory module is loaded:

```powershell-session
Get-Module -Name ActiveDirectory -ListAvailable 
```
