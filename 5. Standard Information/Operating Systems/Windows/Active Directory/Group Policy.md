---
tags:
  - OperatingSystems
  - Windows
  - StandardInformation
  - ActiveDirectory
---

Group Policy is a Windows feature that provides administrators with a wide array of advanced settings that can apply to both user and computer accounts in a Windows environment.

Every Windows host has a Local Group Policy editor to manage local settings. For our purposes, we will focus on Group Policy in a domain context for managing users and computers in Active Directory. Group Policy is a powerful tool for managing and configuring user settings, operating systems, and applications. Group Policy is also a potent tool for managing security in a domain environment. From a security context, leveraging Group Policy is one of the best ways to widely affect your enterprise's security posture.

## Group Policy Objects (GPOs)

A [Group Policy Object (GPO)](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/policy/group-policy-objects) is a virtual collection of policy settings that can be applied to `user(s)` or `computer(s)`. GPOs include policies such as screen lock timeout, disabling USB ports, enforcing a custom domain password policy, installing software, managing applications, customizing remote access settings, and much more. Every GPO has a unique name and is assigned a unique identifier (a GUID). They can be linked to a specific OU, domain, or site. A single GPO can be linked to multiple containers, and any container can have multiple GPOs applied to it. They can be applied to individual users, hosts, or groups by being applied directly to an OU. Every GPO contains one or more Group Policy settings that may apply at the local machine level or within the Active Directory context.















