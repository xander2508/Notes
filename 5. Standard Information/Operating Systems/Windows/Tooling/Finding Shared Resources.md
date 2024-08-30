---
tags:
  - OperatingSystems
  - Windows
  - Tooling
---
One way of doing so involves using the `net share` command. [Net Share](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh750728(v=ws.11)) allows us to display info about shared resources on the host and to create new shared resources as well.

```cmd-session
C:\htb> net share  

Share name   Resource                        Remark

-------------------------------------------------------------------------------
C$           C:\                             Default share
IPC$                                         Remote IPC
ADMIN$       C:\Windows                      Remote Admin
Records      D:\Important-Files              Mounted share for records storage  
The command completed successfully.
```

[Net View](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh875576(v=ws.11)) will display to us any shared resources the host you are issuing the command against knows of. This includes domain resources, shares, printers, and more.
 
```cmd-session
C:\htb> net view  
```
# Things to note

- Do we have the proper permissions to access this share?
- Can we read, write, and execute files on the share?
- Is there any valuable data on the share?