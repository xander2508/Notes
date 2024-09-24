---
tags:
  - OperatingSystems
  - Windows
  - PowerShell
  - Commands
  - StandardInformation
  - Tooling
---
A [cmdlet](https://docs.microsoft.com/en-us/powershell/scripting/lang-spec/chapter-13?view=powershell-7.2) as defined by Microsoft is: "a single-feature command that manipulates objects in PowerShell."

Cmdlets follow a Verb-Noun structure which often makes it easier for us to understand what any given cmdlet does. With Test-WSMan, we can see the `verb` is `Test` and the `Noun` is `Wsman`. The verb and noun are separated by a dash (`-`). After the verb and noun, we would use the options available to us with a given cmdlet to perform the desired action. Cmdlets are similar to functions used in PowerShell code or other programming languages but have one significant difference. Cmdlets are `not` written in PowerShell. They are written in C# or another language and then compiled for use. As we saw in the last section, we can use the `Get-Command` cmdlet to view the available applications, cmdlets, and functions, along with a trait labelled "CommandType" that can help us identify its type.

If we want to see the options and functionality available to us with a specific cmdlet, we can use the [Get-Help](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-help?view=powershell-7.2) cmdlet as well as the `Get-Member` cmdlet.

# Commands 
`Get-Command` is a great way to find a pesky command that might be slipping from our memory right when we need to use it. With PowerShell using the `verb-noun` convention for cmdlets, we can search on either.

```powershell-session
 Get-Command -verb get
```

```powershell-session
Get-Command -noun windows*  
```
