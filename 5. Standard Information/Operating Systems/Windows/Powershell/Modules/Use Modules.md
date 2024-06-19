## Finding Loaded Modules
`Get-Module` can help us determine what modules are already loaded. Allows you to list all loaded modules:

```powershell-session
Get-Module 
```

The `-ListAvailable` modifier will show us all modules we have installed but not loaded into our session.

```powershell-session
Get-Module -ListAvailable 
```


## Importing Modules

The [Import-Module](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/import-module?view=powershell-7.2) cmdlet allows us to add a module to the current PowerShell session.

```powershell-session
Import-Module .\PowerSploit.psd1
```

## Viewing Module Path 

Modules are not loaded if they are not in the loaded module path.

```powershell-session
$env:PSModulePath
```

## Listing Module's Commands 

```powershell-session
Get-Command -Module <modulename>
```

## Finding & Installing Modules

Administrator access required:

When it comes to PowerShell modules, the [PowerShell Gallery](https://www.powershellgallery.com/) Is the best place for finding and installing modules.

List commands related to the PowerShell Gallery:

```powershell-session
Get-Command -Module PowerShellGet 
```

```powershell-session
Find-Module -Name AdminToolbox | Install-Module
```

## Interesting Modules 

- [AdminToolbox](https://www.powershellgallery.com/packages/AdminToolbox/11.0.8): AdminToolbox is a collection of helpful modules that allow system administrators to perform any number of actions dealing with things like Active Directory, Exchange, Network management, file and storage issues, and more.
    
- [ActiveDirectory](https://learn.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2022-ps): This module is a collection of local and remote administration tools for all things Active Directory. We can manage users, groups, permissions, and much more with it.
    
- [Empire / Situational Awareness](https://github.com/BC-SECURITY/Empire/tree/master/empire/server/data/module_source/situational_awareness): Is a collection of PowerShell modules and scripts that can provide us with situational awareness on a host and the domain they are apart of. This project is being maintained by [BC Security](https://github.com/BC-SECURITY) as a part of their Empire Framework.
    
- [Inveigh](https://github.com/Kevin-Robertson/Inveigh): Inveigh is a tool built to perform network spoofing and Man-in-the-middle attacks.
    
- [BloodHound / SharpHound](https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors): [[Bloodhound]]/Sharphound allows us to visually map out an Active Directory Environment using graphical analysis tools and data collectors written in C# and PowerShell.