---
tags:
  - Enumeration
  - TCP
  - ServerMessageBlock
  - SMB
  - Tooling
  - Responder
---
When Responder is used together with MultiRelay, Responder acts like a funnel on the local subnet by tricking victim machines into initiating NTLMv1/v2 authentication requests and sending the requests to MultiRelay, which forwards the authentication requests along to a target machine in a man-in-the-middle condition. If the account that we’ve tricked into trying to authenticate has at least local administrative privileges on the target machine, we can dump local password hashes, launch shells, pivot to other devices, and also use the “reg save” Windows command to save off a copy of the SAM, SYSTEM, and SECURITY hives from the registry of the compromised box, which can be used to extract cached domain password hashes.

> [!NOTE]
> Since the Microsoft [**MS08-068**](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2008/ms08-068) vulnerability patch, you cannot relay NTLMv1/v2 authentication to the same machine from which it came.

1. First you’ll want to identify machines in the network that don’t require SMB signing. Responder has a neat tool packaged with it called [[RunFinger]] that can scan subnets for Windows devices and show if SMB signing is required.
2. Set SMB and HTTP to `OFF` in our responder configuration file (`/etc/responder/Responder.conf`).
3. Run [[1. Responder|Responder]] with options `-rv`
4. Run MultiRelay, see below:

```
python MultiRelay.py -t 10.1.1.100 -u ALL -d
```
If you don’t specify an action to execute, MultiRelay will drop you into a shell on the target machine with a submenu of available options


## Guide

1. [Using MultiRelay with Responder for Penetration Testing](https://www.sikich.com/insight/using-multirelay-with-responder-for-penetration-testing/)