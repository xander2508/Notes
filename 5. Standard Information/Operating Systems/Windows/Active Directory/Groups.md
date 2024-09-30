---
tags:
  - OperatingSystems
  - Windows
  - StandardInformation
  - ActiveDirectory
---
Groups can place similar users together and mass assign rights and access. Groups are another key target for attackers and penetration testers, as the rights that they confer on their members may not be readily apparent but may grant excessive (and even unintended) privileges that can be abused if not set up correctly.

There are many [built-in groups](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-security-groups#about-active-directory-groups) in Active Directory, and most organizations also create their own groups to define rights and privileges, further managing access within the domain. The number of groups in an AD environment can snowball and become unwieldy, potentially leading to unintended access if left unchecked. It is essential to understand the impact of using different group types and for any organization to periodically `audit` which groups exist within their domain, the privileges that these groups grant their members, and check for excessive group membership beyond what is required for a user to perform their day-to-day work.

One question that comes up often is the difference between Groups and Organizational Units (OUs). As discussed earlier in the module, OUs are useful for grouping users, groups, and computers to ease management and deploying Group Policy settings to specific objects in the domain. Groups are primarily used to assign permissions to access resources. OUs can also be used to delegate administrative tasks to a user, such as resetting passwords or unlocking user accounts without giving them additional admin rights that they may inherit through group membership.

## Types of Groups

In simpler terms, groups are used to place users, computers, and contact objects into management units that provide ease of administration over permissions and facilitate the assignment of resources such as printers and file share access.

Every user in a group will inherit the permissions based on their membership in the group. If the permissions need to be modified or revoked for one or more users, they could merely be removed from the group, leaving the other users unaffected and their permissions intact.

Groups in Active Directory have two fundamental characteristics: `type` and `scope`. The `group type` defines the group's purpose, while the `group scope` shows how the group can be used within the domain or forest. When creating a new group, we must select a group type. There are two main types: `security` and `distribution` groups.

- The `Security groups` type is primarily for ease of assigning permissions and rights to a collection of users instead of one at a time. They simplify management and reduce overhead when assigning permissions and rights for a given resource. All users added to a security group will inherit any permissions assigned to the group, making it easier to move users in and out of groups while leaving the group's permissions unchanged.

- The `Distribution groups` type is used by email applications such as Microsoft Exchange to distribute messages to group members. They function much like mailing lists and allow for auto-adding emails in the "To" field when creating an email in Microsoft Outlook. This type of group cannot be used to assign permissions to resources in a domain environment.

---

## Group Scopes

There are three different `group scopes` that can be assigned when creating a new group.

1. Domain Local Group
2. Global Group
3. Universal Group

#### Domain Local Group

Domain local groups can only be used to manage permissions to domain resources in the domain where it was created. Local groups cannot be used in other domains but `CAN` contain users from `OTHER` domains. Local groups can be nested into (contained within) other local groups but `NOT` within global groups.

#### Global Group

Global groups can be used to grant access to resources in `another domain`. A global group can only contain accounts from the domain where it was created. Global groups can be added to both other global groups and local groups.

#### Universal Group

The universal group scope can be used to manage resources distributed across multiple domains and can be given permissions to any object within the same `forest`. They are available to all domains within an organization and can contain users from any domain. Unlike domain local and global groups, universal groups are stored in the Global Catalogue (GC), and adding or removing objects from a universal group triggers forest-wide replication. It is recommended that administrators maintain other groups (such as global groups) as members of universal groups because global group membership within universal groups is less likely to change than individual user membership in global groups. Replication is only triggered at the individual domain level when a user is removed from a global group. If individual users and computers (instead of global groups) are maintained within universal groups, it will trigger forest-wide replication each time a change is made. This can create a lot of network overhead and potential for issues.

Group scopes can be changed, but there are a few caveats:

- A Global Group can only be converted to a Universal Group if it is NOT part of another Global Group.
- A Domain Local Group can only be converted to a Universal Group if the Domain Local Group does NOT contain any other Domain Local Groups as members.
- A Universal Group can be converted to a Domain Local Group without any restrictions.
- A Universal Group can only be converted to a Global Group if it does NOT contain any other Universal Groups as members.

## Built-in vs. Custom Groups

Several built-in security groups are created with a Domain Local Group scope when a domain is created. These groups are used for specific administrative purposes.

It is important to note that only user accounts can be added to these built-in groups as they do not allow for group nesting.












