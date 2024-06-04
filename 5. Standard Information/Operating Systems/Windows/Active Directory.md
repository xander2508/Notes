In a nutshell, `Active Directory` (AD) is a directory service for Windows environments that provides a central point of management for `users`, computers, `groups`, network devices, `file shares`, group policies, `devices`, and trusts with other organizations. Think of it as the gatekeeper for an enterprise environment. Anyone who is a part of the domain can access resources freely, while anyone who is not is denied access to those same resources or, at a minimum, stuck waiting in the visitors centre.


# Managing Domain Users and Groups

`ActiveDirectory` PowerShell Module is required to manage users and groups with PowerShell. Another requirement is to have the optional feature `Remote System Administration Tools` installed

```powershell-session
Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability -Online
```

Ensure the PowerShell Active Directory module is loaded:

```powershell-session
Get-Module -Name ActiveDirectory -ListAvailable 
```

## Listing Users 

```powershell-session
Get-ADUser -Filter *
```

```powershell-session
Get-ADUser -Identity TSilver
```