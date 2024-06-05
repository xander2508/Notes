
# Locally 

```powershell-session
Get-Service | ft DisplayName,Status 
```
```powershell-session
Get-Service | Where-Object {$_.Status -eq "Running"} | ft DisplayName 
```

# Remotely

```powershell-session
Get-Service -ComputerName ACADEMY-ICL-DC
```
```powershell-session
Get-Service -ComputerName ACADEMY-ICL-DC | Where-Object {$_.Status -eq "Running"}
```