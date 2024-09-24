---
tags:
  - Enumeration
  - TCP
  - ServerMessageBlock
  - SMB
  - Concepts
  - Information
---
## Connect from Linux

#### Mount

See [[5. Standard Information/Operating Systems/Linux/Tooling/Default/Mount|Mount]]

> [!NOTE]
> We need to install `cifs-utils` to connect to an SMB share folder. To install it we can execute from the command line `sudo apt install cifs-utils`.

```shell-session
sudo mkdir /mnt/Finance
```

```shell-session
sudo mount -t cifs -o username=plaintext,password=Password123,domain=. //192.168.220.129/Finance /mnt/Finance
```

As an alternative, we can use a credential file.

```shell-session
mount -t cifs //192.168.220.129/Finance /mnt/Finance -o credentials=/path/credentialfile
```

```txt
username=plaintext
password=Password123
domain=.
```
## Connect from Windows

#### GUI

On Windows GUI, we can press `[WINKEY] + [R]` to open the Run dialog box and type the file share location, e.g.: `\\192.168.220.129\Finance\`
#### CMD

```cmd-session
dir \\192.168.220.129\Finance\
```

```cmd-session
net use n: \\192.168.220.129\Finance
```

```cmd-session
net use n: \\192.168.220.129\Finance /user:plaintext Password123
```

#### PowerShell

```powershell-session
Get-ChildItem \\192.168.220.129\Finance\
```

Mount the shared drive as a new file system drive:

```powershell-session
New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem"
```

With credentials:

```powershell-session
$username = 'plaintext'

$password = 'Password123'

$secpassword = ConvertTo-SecureString $password -AsPlainText -Force

$cred = New-Object System.Management.Automation.PSCredential $username, $secpassword

New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem" -Credential $cred
```
