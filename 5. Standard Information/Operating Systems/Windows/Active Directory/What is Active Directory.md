---
tags:
  - OperatingSystems
  - Windows
  - StandardInformation
  - ActiveDirectory
---
TLDR: 
In a nutshell, `Active Directory` (AD) is a directory service for Windows environments that provides a central point of management for `users`, computers, `groups`, network devices, `file shares`, group policies, `devices`, and trusts with other organizations. Think of it as the gatekeeper for an enterprise environment. Anyone who is a part of the domain can access resources freely, while anyone who is not is denied access to those same resources or, at a minimum, stuck waiting in the visitors centre.

AD is essentially a sizeable read-only database accessible to all users within the domain, regardless of their privilege level. A basic AD user account with no added privileges can enumerate most objects within AD. This fact makes it extremely important to properly secure an AD implementation because ANY user account, regardless of their privilege level, can be used to enumerate the domain and hunt for misconfigurations and flaws thoroughly.
## Overview 

Active Directory (AD) is a directory service for Windows network environments. It is a distributed, hierarchical structure that allows for centralized management of an organization's resources, including users, computers, groups, network devices, file shares, group policies, devices, and trusts. AD provides authentication and authorization functions within a Windows domain environment.