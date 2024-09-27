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
