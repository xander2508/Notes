
View all interfaces:

```powershell-session
Get-NetIPInterface
```

Get specific interface:

```powershell-session
Get-NetIPAddress -ifIndex 25
```

Edit interface:

```powershell-session
Set-NetIPInterface -InterfaceIndex 25 -Dhcp Disabled
```

```powershell-session
Set-NetIPAddress -InterfaceIndex 25 -IPAddress 10.10.100.54 -PrefixLength 24
```

Restart adapter:

```powershell-session
Restart-NetAdapter -Name 'Ethernet 3'
```

As long as nothing goes wrong, you will not receive output. Test the connection:

```powershell-session
Test-NetConnection
```