---
tags:
  - Enumeration
  - TCP
  - ServerMessageBlock
  - SMB
  - CIFS
  - CommonInternetFileSystem
  - Applications
---

Samba implements the `Common Internet File System` (`CIFS`) network protocol. [CIFS](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-cifs/934c2faa-54af-4526-ac74-6a24d126724e) is a "dialect" of SMB. In other words, CIFS is a very specific implementation of the SMB protocol, which in turn was created by Microsoft. This allows Samba to communicate with newer Windows systems. Therefore, it usually is referred to as `SMB / CIFS`. However, CIFS is the extension of the SMB protocol. So when we pass SMB commands over Samba to an older NetBIOS service, it usually connects to the Samba server over TCP ports `137`, `138`, `139`, but CIFS uses TCP port `445` only.

With version 3, the Samba server gained the ability to be a full member of an Active Directory domain. With version 4, Samba even provides an Active Directory domain controller. It contains several so-called daemons for this purpose - which are Unix background programs. The SMB server daemon (`smbd`) belonging to Samba provides the first two functionalities, while the [[2. Enumeration/UDP/137. Netbios/1. Guide|NetBios]] message block daemon (`nmbd`) implements the last two functionalities. The SMB service controls these two background programs.


## Configuration 

[smb.conf](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html)