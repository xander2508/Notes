---
tags:
  - OperatingSystems
  - Windows
  - StandardInformation
  - ActiveDirectory
---

Rights and privileges are the cornerstones of AD management and, if mismanaged, can easily lead to abuse by attackers or penetration testers. Access rights and privileges are two important topics in AD (and infosec in general), and we must understand the difference. 

- `Rights` are typically assigned to users or groups and deal with permissions to `access` an object such as a file.
- `privileges` grant a user permission to `perform an action` such as run a program, shut down a system, reset passwords, etc.

Privileges can be assigned individually to users or conferred upon them via built-in or custom group membership. Windows computers have a concept called `User Rights Assignment`, which, while referred to as rights, are actually types of privileges granted to a user.

