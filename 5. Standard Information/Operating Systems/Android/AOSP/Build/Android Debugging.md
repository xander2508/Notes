See also [[LLDB Debugging]] for native generic code
## Live Debugging with Jadex

- **Overview**:
    
    - Jadex is a tool for analyzing Android applications in real time.
    - Useful for reverse engineering and modifying app behavior without recompilation.
- **Case Study: _Call Me Application_**
    
    - Application expects a PIN for authentication.
    - Objective: Bypass the authentication to access a hidden prize URL page.
- **Steps to Debug**:
    
    1. **Launch Jadex**:
        - Use the command `jadex-gui <APK_PATH>` to open the target APK.
        - Locate the main activity of the app (e.g., `com.8ksec.callme.mainactivity`).
    2. **Analyze PIN Logic**:
        - PIN is entered via an `editText` field and validated in the `checkPin()` function.
        - `checkPin()` compares user input with a value returned from the `getPin()` function.
    3. **Set Breakpoints and Intercept Execution**:
        - Attach the debugger to the running application.
        - Identify key points, such as the invocation of `checkPin()`.
    4. **Modify Logic**:
        - **Extract PIN**: Intercept the `getPin()` call and extract its return value (e.g., `1337`).
        - **Flip Logic**: Change the `if-else` condition to treat incorrect PINs as correct.
    5. **Test Changes**:
        - Use the debugger's step-over, step-into, and step-out functionalities to navigate through code execution.
        - Enter manipulated PINs or observe behavior after flipping conditions.
- **Key Features of Jadex**:
    
    - **Step Over**: Execute the current line, skipping detailed method calls.
    - **Step Into**: Delve into the internal logic of a method.
    - **Step Out**: Exit a method and return to its caller.
    - **Breakpoints**: Pause execution at strategic points for live inspection and alteration.

---

## LD Preload in Android

- **Overview**:
    
    - LD Preload is an environment variable used to load custom shared libraries before standard libraries.
    - Enables function overriding for dynamic analysis, debugging, and runtime behavior modification.
- **Capabilities**:
    
    1. **Overriding Constructor and Destructor**:
        - Define custom actions upon library loading (`constructor`) and unloading (`destructor`).
        - Example:
            - **Constructor**: Print process name and ID when the library is loaded.
            - **Destructor**: Perform cleanup operations after the main program exits.
    2. **Overriding Functions**:
        - Replace native library functions with custom implementations.
        - Example: Override `open()` to log or manipulate file paths being accessed.
- **Steps to Use LD Preload**:
    
    1. **Compile Shared Library**:
        
        bash
        
        CopyEdit
        
        `clang -shared -fPIC -o libcustom.so libcustom.c`
        
        - `-shared`: Generate a shared library.
        - `-fPIC`: Create position-independent code suitable for shared libraries.
    2. **Deploy Library to Device**:
        
        bash
        
        CopyEdit
        
        `adb push libcustom.so /data/local/tmp`
        
    3. **Invoke with LD Preload**:
        
        bash
        
        CopyEdit
        
        `LD_PRELOAD=/data/local/tmp/libcustom.so /bin/ls`
        
        - The specified library overrides relevant functions in the `/bin/ls` command.
    4. **Verify Injection**:
        - Use `ldd` to list dependencies of a program and confirm the custom library is loaded:
            
            bash
            
            CopyEdit
            
            `ldd /bin/ls`
            
- **Applications**:
    
    - Debug Android daemons or applications without modifying the APK.
    - Monitor or manipulate API calls during execution.
    - Simulate or extend app functionality dynamically.

---

## Jnitrace: Simplified JNI Monitoring

- **Overview**:
    
    - Jnitrace is a command-line tool that tracks calls between Java code and native libraries in Android applications.
    - Essential for understanding JNI interactions and analyzing native function behavior.
- **Features**:
    
    - Intercepts calls from Java to native libraries and logs details.
    - Can trace specific libraries or all native calls using regex filters.
- **Steps to Use Jnitrace**:
    
    1. **Install Jnitrace**:
        
        bash
        
        CopyEdit
        
        `pip install jnitrace`
        
    2. **Ensure Frida Server is Running**:
        - Push and start the Frida server on the Android device:
            
            bash
            
            CopyEdit
            
            `adb push frida-server /data/local/tmp adb shell su chmod +x /data/local/tmp/frida-server ./frida-server`
            
    3. **Attach Jnitrace**:
        
        bash
        
        CopyEdit
        
        `jnitrace -m attach -l libcallme.so callme`
        
        - `-m attach`: Attach to a running process.
        - `-l`: Specify the library to monitor (e.g., `libcallme.so`).
    4. **Monitor JNI Calls**:
        - Enter a PIN in the app and observe intercepted values in the Jnitrace output.
        - Example: Extract a PIN (`1337`) from a `getPin()` function.
- **Advanced Options**:
    
    - `-i`: Include filters to monitor specific libraries or functions.
    - `-e`: Exclude unwanted data from output.
    - `-R`: Connect to a remote Frida server.
    - `-s`: Spawn a new process instead of attaching to an existing one.
- **Practical Applications**:
    
    - **Reverse Engineering**: Understand how apps use native libraries.
    - **Dynamic Analysis**: Identify vulnerabilities by inspecting native interactions.
    - **Credential Extraction**: Extract sensitive data like PINs or passwords passed through JNI.

---

## Summary of Techniques

- **Smalley Debugging**:
    
    - Enables live analysis and modification of Android applications.
    - Useful for bypassing authentication, inspecting logic, and testing behavior dynamically.
- **LD Preload**:
    
    - Provides runtime manipulation of shared libraries.
    - Ideal for function overriding, logging, and debugging system-level operations.
- **Jnitrace**:
    
    - Simplifies monitoring of Java-to-native interactions.
    - Highly effective for tracing, understanding, and manipulating JNI calls in real time.

These tools are invaluable for penetration testers, security researchers, and developers in analyzing and securing Android applications. Their combined use allows for comprehensive assessment and fine-grained control of app behavior.