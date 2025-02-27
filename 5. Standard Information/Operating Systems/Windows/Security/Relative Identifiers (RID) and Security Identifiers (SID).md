---
tags:
  - OperatingSystems
  - Windows
  - RelativeIdentifiers
  - SecurityIdentifiers
  - RID
  - SID
  - StandardInformation
aliases:
  - RID
  - SID
---

**Relative Identifiers (RID)** and **Security Identifiers (SID)** are key components in Windows operating systems for uniquely identifying and managing objects, such as users and groups, within a network domain.

- **SIDs** serve as unique identifiers for domains, ensuring that each domain is distinguishable.
    
- **RIDs** are appended to SIDs to create unique identifiers for objects within those domains. This combination allows for precise tracking and management of object permissions and access controls.

For instance, a user named `pepe` might have a unique identifier combining the domain's SID with his specific RID, represented in both hexadecimal (`0x457`) and decimal (`1111`) formats. This results in a complete and unique identifier for pepe within the domain like: `S-1-5-21-1074507654-1937615267-42093643874-1111`.

Each of the security principals on the system has a unique security identifier (SID). The system automatically generates SIDs. This means that even if, for example, we have two identical users on the system, Windows can distinguish the two and their rights based on their SIDs. SIDs are string values with different lengths, which are stored in the security database. These SIDs are added to the user's access token to identify all actions that the user is authorized to take.

A SID consists of the Identifier Authority and the Relative ID (RID). In an Active Directory (AD) domain environment, the SID also includes the domain SID.

```powershell-session
PS C:\htb> whoami /user

USER INFORMATION
----------------

User Name           SID
=================== =============================================
ws01\bob S-1-5-21-674899381-4069889467-2080702030-1002
```

The SID is broken down into this pattern.

```powershell-session
(SID)-(revision level)-(identifier-authority)-(subauthority1)-(subauthority2)-(etc)
```

Let's break down the SID piece by piece.

| **Number**                      | **Meaning**          | **Description**                                                                                                                                                                                    |
| ------------------------------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| S                               | SID                  | Identifies the string as a SID.                                                                                                                                                                    |
| 1                               | Revision Level       | To date, this has never changed and has always been `1`.                                                                                                                                           |
| 5                               | Identifier-authority | A 48-bit string that identifies the authority (the computer or network) that created the SID.                                                                                                      |
| 21                              | Subauthority1        | This is a variable number that identifies the user's relation or group described by the SID to the authority that created it. It tells us in what order this authority created the user's account. |
| 674899381-4069889467-2080702030 | Subauthority2        | Tells us which computer (or domain) created the number                                                                                                                                             |
| 1002                            | Subauthority3        | The RID that distinguishes one account from another. Tells us whether this user is a normal user, a guest, an administrator, or part of some other group                                           |
