## Overview

This guide covers the essential techniques for extracting and analyzing Android boot images and firmware files. These skills are critical for:

- **Security researchers**: Identifying vulnerabilities, analyzing system-level operations, and ensuring system security.
- **Developers**: Performing modifications, debugging firmware issues, and understanding the interaction between hardware and software.

---

## **Key Topics Covered**

1. Extracting Android Boot Images
2. Decrypting and Unpacking Firmware Files (OnePlus, Oppo, Pixel)
3. Kernel Extraction from Boot Images
4. Symbolicating the Android Kernel for Reverse Engineering

---

## **1. Extracting Android Boot Images**

### Importance

- **Boot images (`boot.img`)** are essential for understanding Android system initialization and kernel operations.
- Critical for kernel exploitation and custom firmware development.

### Procedure:

1. **Identify Device Fingerprint**:
    
    - Use ADB (Android Debug Bridge) to retrieve the target device fingerprint:
        
        bash
        
        CopyEdit
        
        `adb shell getprop ro.bootimage.build.fingerprint`
        
    - This unique identifier links the device to its corresponding firmware update.
2. **Download the OTA File**:
    
    - Visit the Android OTA Repository.
    - **Steps**:
        - Accept terms and conditions.
        - Locate the device and firmware release (e.g., "cheetah").
        - Right-click the download link, copy the address, and use `wget` to download the file:
            
            bash
            
            CopyEdit
            
            `wget <link_to_OTA_file>`
            
3. **Extract Firmware Images**:
    
    - **Tool**: [OTA Payload Extractor](https://github.com/an-extractor-repo).
    - Clone and install dependencies:
        
        bash
        
        CopyEdit
        
        `git clone <OTA_payload_extractor_repo> pip install -r requirements.txt`
        
    - Extract firmware components:
        
        bash
        
        CopyEdit
        
        `python extract_android_ota_payload.py <OTA_file> <output_directory>`
        
    - Results include files like `boot.img` and `payload.bin`.
4. **Handle `payload.bin` Files**:
    
    - Certain OTA files contain firmware as `payload.bin`. Additional tools, such as Payload Dumper, are required for extraction.

---

## **2. Decrypting and Unpacking Firmware Files**

### Challenges

- Devices like **OnePlus** and **Oppo** use proprietary encrypted firmware formats:
    - `.ops` for OnePlus.
    - `.ofp` for Oppo.
- Decryption is mandatory for analysis.

### Tools and Steps:

1. **Oppo Decrypt Utility**:
    
    - Supports MediaTek and Qualcomm chipsets for OnePlus and Oppo firmware.
    - **Steps**:
        
        1. Clone and install dependencies:
            
            bash
            
            CopyEdit
            
            `git clone <Oppo_decrypt_repo> pip install -r requirements.txt`
            
        2. Unzip the firmware file:
            
            bash
            
            CopyEdit
            
            `unzip <file_name>`
            
        3. Decrypt firmware:
            
            bash
            
            CopyEdit
            
            `python3 ofp_qc_decrypt.py <ofp_file> <output_directory>`
            
        
        - Extracted files include `boot.img`, `system.img`, `vendor.img`, etc.
2. **Utility Functions**:
    
    - Oppo Decrypt also supports re-encrypting firmware for OnePlus devices, aiding in modification and testing.
3. **Verify Extracted Components**:
    
    - Navigate to the output directory and list extracted images:
        
        bash
        
        CopyEdit
        
        `ls *.img`
        
    - Key files to identify include:
        - `boot.img`: Bootloader and kernel.
        - `system.img`: Operating system components.
        - `vendor.img`: Device-specific configurations.

---

## **3. Kernel Extraction from Boot Images**

### Importance

- Extracting the Android kernel provides a deeper understanding of device architecture and low-level operations.
- The kernel is essential for debugging and vulnerability identification.

### Tools and Process:

1. **imj-tool**:
    
    - Free utility to unpack and extract Android boot and system images.
    - Supports multiple proprietary formats.
    - **Download and Setup**:
        
        bash
        
        CopyEdit
        
        `wget <imj_tool_link> tar -xf <tool_file_name>`
        
    - **Extract the Kernel**:
        
        bash
        
        CopyEdit
        
        `./imj-tool boot.img extract`
        
    - The tool generates an extracted directory containing components like the kernel binary.
2. **Decompress Kernel**:
    
    - Android kernels are often compressed (e.g., `lz4`).
    - Decompress using:
        
        bash
        
        CopyEdit
        
        `lz4 -d kernel kernel_extracted`
        
3. **Verify Kernel Version**:
    
    - Check the kernel version to ensure alignment with the target device:
        
        bash
        
        CopyEdit
        
        `strings kernel_extracted | grep "Linux version"`
        

---

## **4. Symbolicating the Android Kernel**

### Purpose

- Symbolication adds meaningful labels (symbols) to kernel binaries, enabling easier analysis.
- This process transforms a raw kernel binary into a human-readable format, facilitating reverse engineering.

### Procedure:

1. **Extract Kernel Symbols**:
    
    - Use the **VM Linux to ELF** tool to convert a raw kernel binary into a symbolicated ELF file.
    - **Setup**:
        
        bash
        
        CopyEdit
        
        `git clone <vmlinux2elf_repo>`
        
    - **Symbolicate the Kernel**:
        
        bash
        
        CopyEdit
        
        `./vmlinux2elf <kernel_file> symbolized_kernel.elf`
        
2. **Verify Symbolication**:
    
    - Use utilities like `nm` or `readelf`:
        
        bash
        
        CopyEdit
        
        `nm symbolized_kernel.elf readelf -a symbolized_kernel.elf`
        
3. **Determine Kernel Base Address**:
    
    - Locate the kernel base using `kalsim_finder`:
        
        bash
        
        CopyEdit
        
        `./kalsim_finder <kernel_file> | grep t_head`
        
4. **Find Symbol Locations**:
    
    - Locate functions like `prepare_kernel_cred`:
        
        bash
        
        CopyEdit
        
        `./kalsim_finder <kernel_file> | grep "prepare_kernel_cred"`
        
    - Calculate offsets for use in exploits:
        
        python
        
        CopyEdit
        
        `print(hex(symbol_address - kernel_base))`
        

---

## **5. Reverse Engineering with Ghidra**

- **Ghidra**: A powerful tool for analyzing and understanding kernel binaries.
- **Loading a Kernel**:
    - Open both raw and symbolicated kernels in Ghidra for comparison.
    - Analyze function calls, memory offsets, and potential vulnerabilities.
- **Symbolicated Kernel Benefits**:
    - Enables navigation of kernel functions and variables.
    - Simplifies vulnerability identification and exploit development.

---

## Tools Overview:

- **OTA Payload Extractor**: Extracts firmware components from OTA files.
- **Oppo Decrypt**: Decrypts OnePlus and Oppo firmware files.
- **imj-tool**: Extracts kernels and system images.
- **VM Linux to ELF**: Symbolicates kernel binaries.
- **Ghidra**: Advanced reverse engineering for Android kernels.

---

## Practical Insights:

- **Symbolicated Kernels**:
    - Provide critical insight into system operations and memory structures.
    - Are indispensable for kernel exploitation and debugging.
- **Heuristic Analysis**:
    - Tools like VM Linux to ELF use heuristic-based pattern recognition to infer symbol locations.
- **Exploit Development**:
    - Understanding offsets and symbol locations aids in crafting reliable exploits for kernel vulnerabilities.

---

## Conclusion:

By mastering these techniques, you will be equipped to:

- Analyze firmware for vulnerabilities.
- Extract and modify Android kernels.
- Reverse engineer kernel binaries to enhance device security.

Now, proceed with hands-on exercises to reinforce these concepts and apply them in real-world scenarios!