---
tags:
  - OperatingSystems
  - Windows
  - Tooling
  - Files
  - StandardInformation
---


```cmd-session
xcopy C:\Users\htb\Documents\example C:\Users\htb\Desktop\ /E
```

```cmd-session
robocopy C:\Users\htb\Desktop C:\Users\htb\Documents\
```

If permissions are insufficient see below, it will overwrite anything in destination directory:

```cmd-session
robocopy /E /MIR /A-:SH C:\Users\htb\Desktop\notes\ C:\Users\htb\Documents\Backup\Files-to-exfil\
```

#### Copy with validation

```cmd-session
 copy calc.exe C:\Users\student\Downloads\copied-calc.exe /V
```