---
tags:
  - Enumeration
  - TCP
  - ServerMessageBlock
  - SMB
  - Concepts
  - AccessControl
  - Information
---
The Windows Defender Firewall may block access to the [[2. Enumeration/TCP/445. Server Message Block (SMB)/1. Guide|SMB]] share.

It is also important to note that when a Windows system is part of a workgroup, all `netlogon` requests are authenticated against that particular Windows system's `SAM` database. When a Windows system is joined to a Windows Domain environment, all netlogon requests are authenticated against `Active Directory`.