See [[5. Standard Information/Operating Systems/Linux/Hardening/SELinux|SELinux]]
## Introduction to SELinux

**Security-Enhanced Linux (SELinux)** is a security architecture integrated into Android and Linux-based systems to enforce **mandatory access control (MAC)** policies. Unlike traditional **discretionary access control (DAC)** systems, SELinux provides granular control over resource access, limiting privilege escalation and mitigating the risk of unauthorized actions by applications and processes.

---

## Comparison: DAC vs. MAC

### Discretionary Access Control (DAC)

- **Ownership-based control**: Resource owners define access permissions.
- **Limitations**:
    - Coarse-grained control.
    - Susceptible to unintended privilege escalations.
    - Access permissions can inadvertently grant excessive rights to processes.

### Mandatory Access Control (MAC)

- **Policy-driven control**: Access decisions are centrally managed using policies.
- **Advantages**:
    - Centralized authority for access decisions.
    - Granular permissions ensure minimal access for processes.
    - Stronger defense against unauthorized resource usage.

---

## SELinux: Core Concepts and Components

### Security Contexts and Labels

SELinux associates every process, file, and resource with a **security context** that defines its security attributes. A security context consists of three components:

1. **User (`u`)**: Specifies the SELinux user, such as `system_u`.
2. **Role (`object_r`)**: Defines the security domain or functional grouping, such as `system_file`.
3. **Type (`t`) or Sensitivity (`s`)**: Specifies the resource's classification level (e.g., `app_data_file`).

**Example Command**:  
`adb shell ls -Z /system`  
Displays the security context of files in the `/system` directory.

### Domains and Types

- **Domains**:
    - Represent processes or system services.
    - Examples: `surfaceflinger_domain`, `untrusted_app_domain`.
- **Types**:
    - Represent resources like files, directories, or sockets.
    - Examples: `app_data_file`, `media_rw_data_file`.

### Sensitivity Levels

- **Default Level**: `S0` for most system files, offering high protection.
- **Higher Levels**: `S1`, `S2`, etc., grant privileged access to specific processes under strict controls.

---

## SELinux Policy Management

SELinux policies define rules governing how processes and resources interact. Policies are compiled into binary files loaded during system startup.

### Types of Policy Files

1. **Public Policies**:
    - Core Android policies provided by AOSP.
    - Govern general system services and processes.
2. **Private Policies**:
    - Device/vendor-specific extensions.
    - May include proprietary modifications.
3. **Vendor Policies**:
    - Policies for third-party drivers and applications.
    - Tailored for hardware-specific implementations.

### `.te` Files (Type Enforcement Files)

- Define rules for domains and types.
- Specify permissions for operations like file access, network communication, and IPC.
- Example:
    
    plaintext
    
    CopyEdit
    
    `allow surfaceflinger app_data_file: file { read write execute };`
    

---

## Advanced SELinux Features

### Policy Attributes

Attributes group related types, simplifying policy management.  
**Example Command**:  
`se-info -a /sys/fs/selinux/policy`  
Lists defined attributes in the SELinux policy.

### Object Classes

Object classes represent resource groupings (e.g., files, sockets, devices).  
**Example Command**:  
`se-info -C /sys/fs/selinux/policy`  
Lists object classes like `bluetooth_socket`, `io_uring`, and `netlink_audit_socket`.

### Policy Capabilities

Fine-grained features that enhance SELinux enforcement.

- **Examples**:
    - `network_peer_controls`: Enforce rules on network communications.
    - `open_perms`: Detailed file permission checks.
- **Command**:  
    `se-info --polcap /sys/fs/selinux/policy`

---

## Key SELinux Commands

### Security Context Inspection

- **Processes**: `adb shell ps -Z`
- **Files**: `adb shell ls -Z`

### Policy Analysis

- **Statistics**:  
    `se-info --stats /sys/fs/selinux/policy`  
    Provides insights like the number of allowed rules and shared domains.
- **Allowed Rules**:  
    `se-search -a /sys/fs/selinux/policy`  
    Lists all permitted operations defined in the policy.

### Rule Filtering

- View rules for specific permissions:
    
    plaintext
    
    CopyEdit
    
    `se-search -t file -p write /sys/fs/selinux/policy`
    
- Focus on kernel rules:
    
    plaintext
    
    CopyEdit
    
    `se-search -s kernel -t file -p read /sys/fs/selinux/policy`
    

---

## SELinux Use Cases and Scenarios

### Application Access Control

- **Without SELinux**: Applications can access resources unchecked, risking data leakage.
- **With SELinux**:
    - Labels ensure access only when explicitly allowed.
    - Example: A social media app cannot access contacts without valid permissions.

### Inter-Process Communication (IPC)

- **Domains for IPC**:
    - `binder_domain`: Manages Android's IPC mechanism.
- **Example**:
    - SurfaceFlinger interacts with other services via IPC while adhering to policy restrictions.

### Managing Media Access

- **Domains**:
    - `media_rw_data_file`: Regulates access to multimedia resources.
- **Example**:
    - A media player can read/write music files but cannot access system-critical directories.

---

## Debugging and Customization Workflow

1. **Identify Device Architecture**:
    - `adb shell getprop` reveals architecture (e.g., `arm64`).
2. **Push Policy Binaries**:
    - Use `adb push` to transfer files to `/data/local/tmp`.
3. **Analyze Policies**:
    - `se-info -a /sys/fs/selinux/policy` for attributes.
4. **Filter Rules**:
    - Use `se-search` with appropriate filters (e.g., source, class, type).

### Example Debugging Session

1. Push binaries:
    
    plaintext
    
    CopyEdit
    
    `adb push arm64/* /data/local/tmp`
    
2. Switch to root:
    
    plaintext
    
    CopyEdit
    
    `su`
    
3. Analyze policy:
    
    plaintext
    
    CopyEdit
    
    `./se-info -a /sys/fs/selinux/policy`
    
4. Filter rules:
    
    plaintext
    
    CopyEdit
    
    `se-search -t file -p read /sys/fs/selinux/policy`
    

---

## SELinux Enhancements and Best Practices

### Fine-Grained Policies

- Utilize sensitivity levels (`S0`-`S2`) to compartmentalize access.
- Define specific rules for high-risk resources.

### Least Privilege Principle

- Assign minimal permissions to applications and processes.
- Regularly review and refine `.te` files.

### Monitoring and Auditing

- Enable logging for denied actions to identify potential issues.
- Use audit tools to trace policy violations.

### Developer Resources

- AOSP directories for public, private, and vendor policies.
- Tools like `SE tools` for in-depth policy analysis.

---

SELinux fortifies Android by implementing robust, flexible, and enforceable security policies. With precise control over resource access, it provides a powerful defense against privilege escalation and unauthorized activities. Mastery of SELinux commands and policies empowers developers and administrators to build highly secure systems tailored to their requirements.