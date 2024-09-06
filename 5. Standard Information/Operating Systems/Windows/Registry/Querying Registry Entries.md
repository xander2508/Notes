---
tags:
  - OperatingSystems
  - Windows
  - Registry
  - StandardInformation
---
From the CLI, we have several options to access the Registry and manage our keys. The first is using [reg.exe](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/reg). `Reg` is a dos executable explicitly made for use in managing Registry settings. The second is using the `Get-Item` and `Get-ItemProperty` cmdlets to read keys and values. If we wish to make a change, the use of New-ItemProperty will do the trick.


# Reg.exe 

```powershell-session
reg query HKEY_LOCAL_MACHINE\SOFTWARE\7-Zip
```

# PowerShell 

```powershell-session
Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | Select-Object -ExpandProperty Property  
```


# Recursive Search 

```powershell-session
Get-ChildItem -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Recurse
```


# Querying Specific Entries

```powershell-session
Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

