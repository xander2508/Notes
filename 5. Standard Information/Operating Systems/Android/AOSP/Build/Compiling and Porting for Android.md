This detailed guide provides a step-by-step breakdown of the process to compile and port exploits for Android devices, ensuring precision at every stage.

---

## 1. **Cross-Compiling for Android**

Cross-compiling is the process of building binaries on a development machine (e.g., a PC) that run on a target platform (e.g., Android devices).

### Steps:

1. **Set Up the Android Native Development Kit (NDK)**:
    
    - **Download Options**:
        - From [NDK official page](https://developer.android.com/ndk/downloads).
        - Through Android Studio:
            - Go to **File > Settings > Appearance & Behavior > System Settings > Android SDK > SDK Tools**.
            - Check **NDK (Side-by-Side)** and **CMake** options.
        - The NDK installation directory is usually located under:
            
            javascript
            
            CopyEdit
            
            `/Users/<username>/Library/Android/sdk/ndk/<version>`
            
    - Verify the installation by checking for the `clang` compiler in the NDK's `toolchains/llvm/prebuilt/<platform>/bin`.
2. **Write the C Program**:
    
    - Example: Create a `hello.c` file with the following content:
        
        c
        
        CopyEdit
        
        `#include <stdio.h> int main() {     printf("Hello, World!\n");     return 0; }`
        
3. **Compile the Code for Android**:
    
    - Use the `clang` compiler from the NDK:
        
        bash
        
        CopyEdit
        
        `./android-clang -target aarch64-linux-android30 hello.c -o hello`
        
        - `-target`: Specifies the architecture (e.g., ARM64).
        - `-o`: Names the output binary.
4. **Transfer and Test**:
    
    - Push the compiled binary to the Android device:
        
        bash
        
        CopyEdit
        
        `adb push hello /data/local/tmp/`
        
    - Connect to the device and execute:
        
        bash
        
        CopyEdit
        
        `adb shell cd /data/local/tmp/ ./hello`
        

---

## 2. **Porting Exploits to Different Devices**

Porting exploits involves adapting them to work on devices with similar hardware but different kernel configurations or offsets.

### Steps:

1. **Analyze the Exploit Code**:
    
    - Identify device-specific hardcoded offsets in the source code.
    - For example, offsets for kernel functions like `selinux_enforcing` or `init_task` often vary between devices.
2. **Download Target Device Firmware**:
    
    - Determine the exact firmware version of the target device:
        
        bash
        
        CopyEdit
        
        `adb shell getprop ro.build.fingerprint`
        
    - Use the fingerprint to find and download the corresponding OTA file from: [https://developers.google.com/android/ota](https://developers.google.com/android/ota).
3. **Extract Boot Image**:
    
    - Use tools like `extract_android_ota_payload` to extract boot images:
        
        bash
        
        CopyEdit
        
        `python3 extract_android_ota_payload.py --input <OTA_file> --output <output_folder>`
        
    - Extract important files like `boot.img`.
4. **Extract the Kernel**:
    
    - Use `android-boot-image-editor` to unpack the `boot.img`:
        
        bash
        
        CopyEdit
        
        `./gradlew unpack --input boot.img --output unpacked_folder`
        
    - Decompress the kernel (if compressed):
        
        bash
        
        CopyEdit
        
        `lz4 -d kernel.lz4 kernel_uncompressed`
        
5. **Symbolize the Kernel**:
    
    - Use `vmlinux-to-elf` to generate symbolic kernel files:
        
        bash
        
        CopyEdit
        
        `./vmlinux-to-elf kernel_uncompressed symbolic_kernel.elf`
        
    - Load the symbolic kernel in tools like Ghidra or IDA Pro to locate kernel functions and addresses.
6. **Update Offsets**:
    
    - For each hardcoded function or memory address in the exploit:
        1. Search for the function (e.g., `selinux_enforcing`) in Ghidra.
        2. Note its address and calculate the offset relative to the kernel base:
            
            python
            
            CopyEdit
            
            `offset = function_address - kernel_base`
            
        3. Replace the old offsets in the exploit with the new ones.
7. **Test the Updated Exploit**:
    
    - Compile the modified exploit using the `make` command.
    - Push the binary to the device and test it:
        
        bash
        
        CopyEdit
        
        `adb push exploit /data/local/tmp/ adb shell cd /data/local/tmp/ ./exploit`
        

---

## 3. **Debugging and Error Handling**

Debugging is essential when the exploit does not behave as expected.

### Common Issues:

1. **Fortify Error**:
    
    - The system’s runtime library may prevent execution.
    - Add the following flags to the compiler options in `Android.mk`:
        
        diff
        
        CopyEdit
        
        `-U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=0`
        
2. **Incorrect Offsets**:
    
    - If the exploit fails, verify all offsets.
    - Recalculate offsets using symbolic analysis tools.
3. **System Reboots or Crashes**:
    
    - Indicates critical errors in the exploit, often due to incorrect addresses or function logic.
    - Revisit the exploit code and firmware analysis.

---

## 4. **Practical Workflow: Porting CVE-2020-0041**

The CVE-2020-0041 exploit is used as an example for porting:

- **Original Target**: Pixel 3 (February 2020 firmware).
- **Port Target**: Pixel 3A XL.

### Process:

1. **Analyze the Exploit Code**:
    
    - Open `exploit.c` and locate hardcoded offsets.
    - Identify kernel functions such as `selinux_enforcing` and `init_task`.
2. **Extract Firmware and Symbolize Kernel**:
    
    - Download OTA file for Pixel 3A XL.
    - Extract kernel and symbolize using `vmlinux-to-elf`.
3. **Update Offsets**:
    
    - Find the addresses for each required function in Ghidra.
    - Calculate the offsets relative to the kernel base and update the exploit.
4. **Compile and Test**:
    
    - Compile the exploit using `make`.
    - Push the binary to the device and execute:
        
        bash
        
        CopyEdit
        
        `adb push poc /data/local/tmp/ adb shell cd /data/local/tmp/ ./poc`
        
5. **Verify Success**:
    
    - Check for root access:
        
        bash
        
        CopyEdit
        
        `id`
        
    - Access restricted directories (e.g., `/data/data`).

---

## Key Takeaways

- **Cross-Compiling**: Simplifies building binaries for Android architectures.
- **Porting Exploits**: Involves precise adjustments to offsets and configurations.
- **Symbolization**: Critical for identifying kernel-level details.
- **Testing and Debugging**: Iterative testing ensures the exploit works as intended.

By mastering these steps, you can adapt and build effective Android exploits across various devices.