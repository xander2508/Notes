---
tags:
  - Enumeration
  - TCP
  - RemoteDesktopProtocol
  - RDP
  - Concepts
  - Vulnerabilities
---
If a user is connected via RDP to our compromised machine, we can hijack the user's remote desktop session to escalate our privileges and impersonate the account. In an Active Directory environment, this could result in us taking over a Domain Admin account or furthering our access within the domain.

![[Pasted image 20240926142900.jpg]]

To successfully impersonate a user without their password, we need to have `SYSTEM` privileges and use the Microsoft [tscon.exe](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/tscon) binary that enables users to connect to another desktop session.

It works by specifying which `SESSION ID` (`4` for the `lewen` session in our example) we would like to connect to which session name (`rdp-tcp#13`, which is our current session). So, for example, the following command will open a new console as the specified `SESSION_ID` within our current RDP session:

```cmd-session
tscon #{TARGET_SESSION_ID} /dest:#{OUR_SESSION_NAME}
```

If Local Administrator permissions are available but SYSTEM is required, see [[Elevating Local Admin to SYSTEM]]


























