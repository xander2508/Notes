## Introduction to Android Generic Kernel Image (GKI)

- The **Android Generic Kernel Image (GKI)** streamlines kernel creation and maintenance for Android devices.
    
- The GKI separates the **core kernel code** from **device-specific components**, allowing faster and more consistent updates.
    
- GKI forms part of Google's strategy to reduce fragmentation in Android kernel development.
    
- It ensures that Android devices running different hardware can share the same **core kernel** without conflicts.
    
- GKI enables rapid security updates, minimizing device vulnerabilities.
    

---

## GKI Project Overview

- GKI is built using the **Android Common Kernel (ACK)** source tree.
    
- Key goals of the GKI:
    
    - Streamline kernel updates.
        
    - Maintain compatibility across hardware vendors.
        
    - Avoid breaking user space functionality.
        
- GKI delivers **single-binary kernels** that are universally applicable to supported devices.
    
- The project also supports **loadable modules** for various architectures and Long-Term Support (LTS) kernel versions.
    
- **Why GKI is Important**:
    
    - Historically, Android devices required custom kernels per device, increasing development burden.
        
    - GKI provides a standardized and unified approach to kernel development, benefiting manufacturers and developers alike.
        

---

## GKI Architecture

- **Core Structure**:
    
    - GKI includes a unified boot image containing:
        
        - **Kernel binary** (single-binary kernel).
            
        - **Loadable modules**: Architecturally specific modules.
            
    - It allows the separation of hardware-agnostic and hardware-specific code.
        
- **Key Components**:
    
    - Core kernel code: Updated frequently.
        
    - Vendor modules: Device-specific.
        
    - Updates to the core kernel do not require changes to vendor images.
        
- **Boot Image**:
    
    - A boot image (e.g., `boot.img`) can be flashed directly using the `fastboot` tool.
        
    - GKI reduces the need to modify device-specific images.
        

---

## Advantages of GKI

1. **Simplified Updates**:
    
    - Updates to the core kernel do not disrupt vendor modules.
        
    - Ensures stability and compatibility.
        
2. **Improved Maintenance**:
    
    - A single update can benefit all supported devices.
        
3. **Flexibility**:
    
    - Developers can flash prebuilt GKI kernels to supported devices for security research and testing.
        
4. **Reduced Fragmentation**:
    
    - Consistent kernel builds across devices reduce variations in Android kernel versions.
        
5. **Enhanced Security**:
    
    - Centralized kernel updates ensure that security patches can be delivered faster.
        

---

## Release Stages in GKI

### Respin

- A **respin** is a process of creating a **new build** of an existing GKI prebuilt kernel.
    
- It involves rebuilding the kernel with:
    
    - Bug fixes.
        
    - New feature additions.
        
    - Upgrades to a newer kernel version.
        
- **Why Respin is Necessary**:
    
    - As the Android ecosystem evolves, bugs or vulnerabilities may emerge in existing kernels.
        
    - Instead of creating an entirely new kernel, respins offer a lightweight and efficient way to deploy fixes.
        
- **Example of Respin Use Case**:
    
    - A security vulnerability is identified in an older GKI release.
        
    - Google applies a patch and respins the kernel to release a fixed version quickly.
        

### Deprecated Releases

- **Deprecated GKI builds** are no longer supported by Google.
    
- Deprecated versions should not be used for new development purposes.
    
- These versions are often retained for historical analysis, testing, or backward compatibility.
    

---

## Kernel Artifacts

When downloading GKI releases, several kernel artifacts are provided:

1. **Kernel Image Files**:
    
    - `image`:
        
        - The kernel binary file.
            
    - `image.gz`:
        
        - Gzip-compressed kernel binary.
            
    - `image.lz4`:
        
        - LZ4-compressed kernel binary.
            
2. **Boot Image**:
    
    - `boot.img`: Contains an uncompressed kernel binary for booting.
        
3. **System.map**:
    
    - Lookup table for kernel symbols and their memory addresses.
        
    - Useful for:
        
        - Debugging.
            
        - Kernel research.
            
        - Exploitation.
            
4. **Modules**:
    
    - `modules.builtin`:
        
        - List of all modules built into the kernel.
            
        - Used by the `modprobe` tool.
            
5. **vmlinux**:
    
    - A statically linked executable containing the Linux kernel.
        
    - Useful for:
        
        - Debugging kernel binaries.
            
6. **vmlinux.symvers**:
    
    - A list of all symbols included in the `vmlinux` binary.
        
    - Useful for reverse engineering and analysis.
        

---

## Flashing GKI Images

- **Fastboot Command**: To flash GKI images to a target device:
    
    ```
    fastboot boot <boot.img>
    ```
    
    - Replace `<boot.img>` with the downloaded boot image file.
        
- This command allows seamless flashing of GKI kernels onto supported Android devices.
    

---

## Accessing Older GKI Images

- Older GKI releases can be downloaded and flashed onto devices.
    
- This is particularly useful for:
    
    - Testing compatibility.
        
    - Kernel research.
        
    - Debugging specific kernel versions.
        
- **Process**:
    
    - Download the desired GKI image.
        
    - Use `fastboot` to flash the image to the device.
        

---

## Key Terminologies

- **GKI**: Android Generic Kernel Image.
    
- **ACK**: Android Common Kernel, the source tree used to build GKI.
    
- **Respin**: Rebuilding an existing GKI prebuilt.
    
- **Deprecated Builds**: Outdated and unsupported GKI releases.
    
- **System.map**: Kernel symbols lookup table.
    
- **Modules.builtin**: Built-in kernel modules list.
    
- **vmlinux**: Debuggable Linux kernel binary.
    
- **vmlinux.symvers**: Kernel symbols dump.
    

---

## Summary

By separating the core kernel from vendor-specific components, GKI simplifies Android kernel development. Key benefits include easier updates, reduced fragmentation, and universal compatibility for supported devices. Through tools like **Fastboot**, developers can seamlessly flash GKI boot images to target devices, enabling advanced testing, research, and maintenance workflows.