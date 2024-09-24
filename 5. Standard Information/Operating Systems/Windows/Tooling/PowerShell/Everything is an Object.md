---
tags:
  - OperatingSystems
  - Windows
  - PowerShell
  - StandardInformation
  - Tooling
---
With PowerShell, not everything is generic text strings like in Bash or cmd. In PowerShell everything is an object instead of a generic string and therefore has methods and properties.

# Get-Member

Get-Member is a cmdlet in PowerShell that allows users to retrieve information about the properties and methods of an object. It provides a list of all the members (properties and methods) that are available for a specific object, allowing users to explore and understand the structure of the object.

```powershell-session
Get-LocalUser administrator | Get-Member
```

```
Get-Member <cmdlet>
```
## Select-Object 

```powershell-session
Get-LocalUser administrator | Select-Object -Property *
```

Filter on object properties

```powershell-session
Get-LocalUser * | Select-Object -Property Name,PasswordLastSet
```

Sort based on properties 

```powershell-session
Get-LocalUser * | Sort-Object -Property Name | Group-Object -property Enabled
```

Reduce and format large outputs 

```powershell-session
Get-Service | Select-Object -Property DisplayName,Name,Status | Sort-Object DisplayName | fl
```

Reverse command output:

```
tasklist | sort /R
```
## Evaluation of Objects 

`Where` and many other cmdlets can `evaluate` objects and data based on the values those objects and their properties contain.

```powershell-session
 Get-Service | where DisplayName -like '*Defender*'
```

#### Comparison Operators

|**Expression**|**Description**|
|---|---|
|`Like`|Like utilizes wildcard expressions to perform matching. For example, `'*Defender*'` would match anything with the word Defender somewhere in the value.|
|`Contains`|Contains will get the object if any item in the property value matches exactly as specified.|
|`Equal` to|Specifies an exact match (case sensitive) to the property value supplied.|
|`Match`|Is a regular expression match to the value supplied.|
|`Not`|specifies a match if the property is `blank` or does not exist. It will also match `$False`.|
[about Comparison Operators - PowerShell | Microsoft Learn](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-7.2)

#### Filtering using Where

```powershell-session
 Get-Service | where DisplayName -like '*Defender*' | Select-Object -Property *
```
