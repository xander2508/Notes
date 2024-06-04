In a nutshell, `Active Directory` (AD) is a directory service for Windows environments that provides a central point of management for `users`, computers, `groups`, network devices, `file shares`, group policies, `devices`, and trusts with other organizations. Think of it as the gatekeeper for an enterprise environment. Anyone who is a part of the domain can access resources freely, while anyone who is not is denied access to those same resources or, at a minimum, stuck waiting in the visitors centre.


# Managing Domain Users and Groups

`ActiveDirectory` PowerShell Module is required to manage users and groups with PowerShell. Another requirement is to have the optional feature `Remote System Administration Tools` installed

```powershell-session
Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability -Online
```

Ensure the PowerShell Active Directory module is loaded:

```powershell-session
Get-Module -Name ActiveDirectory -ListAvailable 
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

We can see from the output several pieces of information about the user, including:

- `Object Class`: which specifies if the object is a user, computer, or another type of object.
- `DistinguishedName`: Specifies the object's relative path within the AD schema.
- `Enabled`: Tells us if the user is active and can log in.
- `SamAccountName`: The representation of the username used to log into the ActiveDirectory hosts.
- `ObjectGUID`: Is the unique identifier of the user object.


## Creating New Users

```powershell-session
New-ADUser -Name "MTanaka" -Surname "Tanaka" -GivenName "Mori" -Office "Security" -OtherAttributes @{'title'="Sensei";'mail'="MTanaka@greenhorn.corp"} -Accountpassword (Read-Host -AsSecureString "AccountPassword") -Enabled $true 
```

- `New-ADUser -Name "MTanaka"` : We issue the `New-ADUser` command and set the user's SamAccountName to `MTanaka`.
- `-Surname "Tanaka" -GivenName "Mori"`: This portion sets our user's `Lastname` and `Firstname`.
- `-Office "Security"`: Sets the extended property of `Office` to `Security`.
- `-OtherAttributes @{'title'="Sensei";'mail'="MTanaka@greenhorn.corp"}`: Here we set other extended attributes such as `title` and `Email-Address`.
- `-Accountpassword (Read-Host -AsSecureString "AccountPassword")`: With this portion, we set the user's `password` by having the shell prompt us to enter a new password. (we can see it in the line below with the stars)
- `-Enabled $true`: We are enabling the account for use. The user could not log in if this was set to `\$False`.