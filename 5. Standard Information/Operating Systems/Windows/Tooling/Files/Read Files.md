---
tags:
  - OperatingSystems
  - Windows
  - Tooling
  - Files
  - StandardInformation
---
# PowerShell 

```
Get-Content
```
# More 

Show a percentage of the file at one time using ENTER to scroll through.

```
more a.txt
```

To remove blank space:

```
more /S a.txt
```

Sending a Command Output to More

```cmd-session
ipconfig /all | more
```


# Type

Read the entire file at once.

```
type a.txt
```

```cmd-session
type passwords.txt >> secrets.txt
```


