# Android Bootloader Course: Symbolizing Crash Logs

## Overview
Symbolizing crash logs is a critical step in debugging Android applications. Manually analyzing tombstone files is time-consuming and prone to errors. This guide explains how to use tools like `NDK stack` and `address-to-line` utilities to convert raw memory addresses into human-readable function names and line numbers.

---

## Step-by-Step Process

### **Extracting Relevant Files**
1. **Locate and Extract `so` Files**
   - Use `adb pull` to download the target APK file from the device.
   - Unzip the APK to access the `lib` directory.
   - Navigate to `lib/arm64` (or the relevant architecture directory).
   - Locate the target `.so` file (e.g., `libbuggycrash.so`).

### **Reading and Symbolizing Files**
2. **Using `nm` Utility (Optional)**
   - Use `nm` to read the extracted `.so` file for offset and symbol details.
   - Identify `JNI` calls or other function names.

3. **Using LLVM's `address-to-line` Utility**
   - Locate the utility in the extracted Android NDK folder:
     ```
     find . -iname "*address-to-line*"
     ```
   - Run the utility with relevant options:
     ```
     ./llvm-addr2line -C -f -e <path-to-so-file> <function-offset>
     ```
     - `-C`: Demangles function names.
     - `-f`: Points to the specific function causing the crash.
     - `-e`: Specifies the `.so` file path.
   - This outputs:
     - Function name causing the crash.
     - File and line number of the crash.

---

### **Interpreting Crash Logs**
4. **Analyze the Crash Location**
   - Example:
     - Function: `native_crash_2`
     - File: `native_lib.cpp`
     - Line: `27`
   - Error: Buffer overflow due to improper memory handling (`strcpy` used with a buffer size mismatch).

---

## Debugging with NDK Stack

### **Setting Up**
1. Locate the `ndk-stack` utility:
	`find . -iname "ndk-stack"`
2. Note the path to `ndk-stack` and the symbol file directory.

### **Symbolizing Tombstone Files**
1. Run the following command:
	`./ndk-stack -sym <path-to-symbol-directory> -dump <path-to-tombstone-file>`
- `-sym`: Specifies the directory containing symbols.
- `-dump`: Specifies the path to the tombstone file.

2. Output:
- Full stack trace with file names and line numbers.
- Pinpointed function and code causing the crash.

---

## Common Crash Example
### **Error Analysis**
- **Buffer Overflow:**
- Code: 
 ```cpp
 strcpy(buffer, keystrings);
 ```
- Problem:
 - `buffer` size: 16 bytes.
 - `keystrings` size exceeds 16 bytes, causing overflow.

### **Solution**
- Use safer memory functions (e.g., `strncpy`).
- Ensure buffer sizes are adequate for input data.

---

## Utility Options Summary

### **Address-to-Line Options**
- `-C`: Demangles names.
- `-f`: Locates specific functions.
- `-e`: Specifies the `.so` file.

### **NDK-Stack Options**
- `-sym`: Points to the symbol directory.
- `-dump`: Specifies the tombstone file path.

---

## Key Takeaways
- Symbolizing crash logs saves time and provides detailed insights into application crashes.
- Tools like `address-to-line` and `ndk-stack` are essential for identifying the root cause.
- Proper memory management in native code prevents common crashes like buffer overflows.

