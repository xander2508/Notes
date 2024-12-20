---
tags:
  - OperatingSystems
  - Linux
  - Hardening
  - StandardInformation
---
SELinux is a MAC system that is built into the Linux kernel. It is designed to provide fine-grained access control over system resources and applications. SELinux works by enforcing a policy that defines the access controls for each process and file on the system. It provides a higher level of security by limiting the damage that a compromised process can do.

 In SELinux, every process, file, directory, and system object is given a label. Policy rules are created to control access between these labelled processes and objects and are enforced by the kernel. This means that access can be set up to control which users and applications can access which resources. SELinux provides very granular access controls, such as specifying who can append to a file or move it.

### Introduction to SELinux

- **Importance of SELinux**: SELinux enforces robust security on Android devices by implementing Mandatory Access Control (MAC), protecting applications and system resources from unauthorized access and vulnerabilities.
- **Difference Between DAC and MAC**:
    - **DAC (Discretionary Access Control)**: Relies on ownership for access permissions, prone to privilege escalation.
    - **MAC (Mandatory Access Control)**: Uses a centralized policy to decide access attempts, offering stricter control.

---

### Key SELinux Concepts

#### SELinux Security Context Labels

- Labels consist of **User, Role, Type, and Sensitivity Level**.
- **Viewing Labels**:
    - Command: `adb shell ls -Z /system` - Displays directory or file security context labels.
    - `adb shell ps -Z` - Shows security labels of processes.
- **Components of Labels**:
    - **User (`u`)**: SELinux user associated with the object.
    - **Role (`r`)**: Domain for the object (e.g., `system_file_r` for protected system files).
    - **Type (`t`)**: Defines object interaction domains (e.g., `app_data_file` for app-specific data).
    - **Sensitivity (`s`)**: Security level (e.g., `s0` for default protection).

#### SELinux Policy Files

- **Type Enforcement (.te) Files**:
    - Define security contexts and rules for domain interactions.
    - Example: `surfaceflinger.te` grants specific permissions for managing frame buffers and display resources.
    - Rules specify operations like reading, writing, and creating objects.
- **Policy Directories**:
    - **public/**: Core system services, provided by AOSP.
    - **private/**: Vendor-specific or proprietary services.
    - **vendor/**: Components like drivers and system applications outside the core Android platform.

---

### Tools and Commands for Policy Analysis

#### Policy Analysis Tools

- **Setools**:
    - Commands: `seinfo`, `sesearch`.
    - Example: `seinfo -a /sys/fs/selinux/policy` - Lists security attributes.
- **ADB Commands**:
    - Push tools using `adb push` for device interaction.
    - Root access (`su`) required for some operations.

#### Policy Queries and Interpretations

- **View Allowed Rules**: `sesearch -A /sys/fs/selinux/policy`.
- **Filter Rules**:
    - Example: View rules for `media_rw_data_file` type allowing `read`:
        
        bash
        
        Copy code
        
        `sesearch -A -t media_rw_data_file -c file -p read /sys/fs/selinux/policy`
        
    - Filter by source (e.g., kernel rules): `sesearch -A -s kernel`.

#### Object Classes and Capabilities

- **Object Classes**:
    - Group objects by type and permissions (e.g., `bluetooth_socket`, `netlink_audit_socket`).
    - Example Command: `seinfo -c /sys/fs/selinux/policy`.
- **Policy Capabilities**:
    - Define fine-grained controls (e.g., network peer communications).
    - Example: `seinfo --polcap /sys/fs/selinux/policy`.

---

### Practical Applications and Insights

- **Boot Time**:
    - SELinux assigns security labels to all files and processes.
- **Real-world Scenarios**:
    - Applications are restricted from accessing resources without proper permissions.
    - Example: Contact access by social media apps is controlled by comparing process labels against resource labels.
- **Custom Policy Adjustments**:
    - Developers can create or modify `.te` files to add permissions or refine domain rules.

---

### Advanced Features and Statistics

- **Policy Rules**:
    - Analyze rule statistics: `seinfo --stats /sys/fs/selinux/policy`.
    - Examples:
        - Allowed Rules: ~3239.
        - Audit Generating Rules: ~89.
        - Suppressed Audit Rules: ~1110.
- **Attributes and Categories**:
    - Simplify permissions management by grouping types.
    - Use `seinfo -a` to explore available attributes.

---

### Conclusion

- **SELinux in Practice**: Protects Android by ensuring processes and resources interact securely.
- **Tools Mastery**: Commands like `adb`, `seinfo`, and `sesearch` are invaluable for policy inspection and refinement.
- **Best Practices**:
    - Maintain minimal permissions for applications.
    - Regularly audit and update SELinux policies for evolving security needs.

By mastering SELinux, developers and security professionals can significantly enhance the security posture of Android devices.