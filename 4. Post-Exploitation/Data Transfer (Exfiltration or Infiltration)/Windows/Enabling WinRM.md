---
tags:
  - Post-Exploitation
  - DataTransfer
  - Windows
---
[Windows Remote Management (WinRM)](https://docs.microsoft.com/en-us/windows/win32/winrm/portal) can be configured using dedicated PowerShell cmdlets and we can enter into a PowerShell interactive session as well as issue commands on remote Windows target(s). We will notice that WinRM is more commonly enabled on Windows Server operating systems, so IT admins can perform tasks on one or multiple hosts. It's enabled by default in Windows Server.

When [[Windows Remote Management (WinRM)]] is enabled on a Windows target, it listens on logical ports `5985` & `5986`.


WinRM can be enabled on a Windows target using the following commands:

```powershell-session
winrm quickconfig
```

As long as credentials to access the system are known, anyone who can reach the target over the network can connect after that command is run.

Once we have enabled and configured WinRM, we can test remote access using the [Test-WSMan](https://docs.microsoft.com/en-us/powershell/module/microsoft.wsman.management/test-wsman?view=powershell-7.2) PowerShell cmdlet.

```powershell-session
Test-WSMan -ComputerName "10.129.224.248"
```

```powershell-session
Test-WSMan -ComputerName "10.129.224.248" -Authentication Negotiate
```