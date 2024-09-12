---
tags:
  - OperatingSystems
  - Windows
  - Security
  - StandardInformation
---


![](https://academy.hackthebox.com/storage/modules/147/authn_credman_credprov.png)

> [!SOURCE]
> [Microsoft Docs](https://docs.microsoft.com/en-us/windows-server/security/windows-authentication/credentials-processes-in-windows-authentication).

Credential Manager is a feature built-in to all Windows operating systems that allows users to save the credentials they use to access various network resources and websites. Saved credentials are stored based on user profiles in each user's `Credential Locker`. Credentials are encrypted and stored at the following location:

  Credential Storage

```powershell-session
PS C:\Users\[Username]\AppData\Local\Microsoft\[Vault/Credentials]\
```

There are various methods to decrypt credentials saved using Credential Manager. We will practice hands-on with some of these methods in this module.