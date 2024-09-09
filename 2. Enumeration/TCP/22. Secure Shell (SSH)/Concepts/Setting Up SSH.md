---
tags:
  - Enumeration
  - TCP
  - SSH
  - SecureShell
  - Concepts
---

We can set up an SSH server on a Windows target using the [Add-WindowsCapability](https://docs.microsoft.com/en-us/powershell/module/dism/add-windowscapability?view=windowsserver2022-ps) cmdlet and confirm that it is successfully installed using the [Get-WindowsCapability](https://docs.microsoft.com/en-us/powershell/module/dism/get-windowscapability?view=windowsserver2022-ps) cmdlet.

Install [[OpenSSH]]:

```powershell-session
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

```powershell-session
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
```

```powershell-session
 Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

Once we have confirmed SSH is installed, we can use the [Start-Service](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/start-service?view=powershell-7.2) cmdlet to start the SSH service. We can also use the [Set-Service](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/set-service?view=powershell-7.2) cmdlet to configure the startup settings of the SSH service if we choose.

```powershell-session
Start-Service sshd  
```

```powershell-session
Set-Service -Name sshd -StartupType 'Automatic'  
```