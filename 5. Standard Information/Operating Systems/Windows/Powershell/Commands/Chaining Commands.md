---
tags:
  - OperatingSystems
  - Windows
  - PowerShell
  - Commands
  - StandardInformation
---
> [!NOTE]
> Currently, Windows PowerShell 5.1 and older do not support Pipeline Chain Operators used in this fashion. If you see errors, you must install PowerShell 7 alongside Windows PowerShell. They are not the same thing.


# Traditional Chaining Commands 

```powershell-session
Get-Process | sort | unique | measure-object
```


# Pipeline Chain Operators

 PowerShell allows us to have conditional execution of pipelines with the use of `Chain operators`. These operators ( `&&` and `||` ) serve two main functions:

- `&&`: Sets a condition in which PowerShell will execute the next command inline `if` the current command `completes properly`.
- `||`: Sets a condition in which PowerShell will execute the following command inline `if` the current command `fails`.