---
tags:
  - OperatingSystems
  - Windows
  - Services
  - StandardInformation
---

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

## Listing Users 

```powershell-session
Get-ADUser -Filter *
```

Searching based on the identity:

```powershell-session
Get-ADUser -Identity TSilver
```

Searching based on an attribute:

```powershell-session
Get-ADUser -Filter {EmailAddress -like '*greenhorn.corp'}
```

```powershell-session
Get-ADUser -Filter {GivenName -like 'robert'}
```

We can see from the output several pieces of information about the user, including:

- `Object Class`: which specifies if the object is a user, computer, or another type of object.
- `DistinguishedName`: Specifies the object's relative path within the AD schema.
- `Enabled`: Tells us if the user is active and can log in.
- `SamAccountName`: The representation of the username used to log into the ActiveDirectory hosts.
- `ObjectGUID`: Is the unique identifier of the user object.