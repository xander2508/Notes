---
tags:
  - OperatingSystems
  - Windows
  - RelativeIdentifiers
  - SecurityIdentifiers
  - RID
  - SID
---

**Relative Identifiers (RID)** and **Security Identifiers (SID)** are key components in Windows operating systems for uniquely identifying and managing objects, such as users and groups, within a network domain.

- **SIDs** serve as unique identifiers for domains, ensuring that each domain is distinguishable.
    
- **RIDs** are appended to SIDs to create unique identifiers for objects within those domains. This combination allows for precise tracking and management of object permissions and access controls.

For instance, a user named `pepe` might have a unique identifier combining the domain's SID with his specific RID, represented in both hexadecimal (`0x457`) and decimal (`1111`) formats. This results in a complete and unique identifier for pepe within the domain like: `S-1-5-21-1074507654-1937615267-42093643874-1111`.