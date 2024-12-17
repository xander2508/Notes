## 1. Introduction to Init and Zygote

- **Init Process**: The first process to start during the Android boot sequence.
    
    - Responsible for creating the **Zygote process**.
        
    - Zygote initializes the **system server** and spawns new processes as needed.
        
- **Key Responsibilities**:
    
    1. Initialization of Android Runtime (ART) or Dalvik Virtual Machine.
        
    2. Creation of Application Processes.
        
    3. Launching the **System Server**.
        
- Processes are created efficiently using the **fork()** system call.
    

---

## 2. Zygote: Role and Functionality

- **What is Zygote?**
    
    - A core component responsible for creating and managing Android processes.
        
    - Employs a **forking mechanism** for efficient creation of processes.
        
    - Spawns application processes and the **system server**.
        
- **Inheritance of Dalvik/ART**:
    
    - Zygote initializes the ART/Dalvik runtime during the boot process.
        
    - Child processes inherit this runtime instance.
        
- **Why Forking is Efficient?**
    
    - Forking avoids the overhead of creating processes from scratch.
        
    - The parent Zygote process is preloaded with system libraries, resources, and the runtime.
        
    - Child processes share these resources, reducing memory usage and startup time.
        
- **Process Duplication**:
    
    - `fork()` creates a near-identical copy of the parent process.
        
    - The child process starts execution where the fork occurs, inheriting the initialized runtime environment.
        

---

## 3. Android Boot Sequence

### Code Analysis

1. **Init Process**:
    
    - Starts via the `init.cpp` file in the Android Source Code.
        
    - Key Function: `load_boot_scripts` (found at **line 335**).
        
    - References the `init.rc` script.
        
2. **Boot Script Details**:
    
    - `init.rc` includes references to other configuration files like:
        
        - `init.zygote.rc`
            
        - `init.zygote64.rc` (for ARM64 devices).
            
3. **Commands to Start Zygote**:
    
    ```
    service zygote /system/bin/app_process64 -Xzygote /system/bin --zygote --start-system-server --socket-name=zygote
    ```
    
    - **Key Flags**:
        
        - `--zygote`: Runs in zygote mode for efficient forking.
            
        - `--start-system-server`: Launches the System Server.
            
        - Path: `/system/bin/app_process64`
            

---

## 4. Key Configuration Files

### **1.** `**init.rc**`

- **Purpose**: The main init script that references additional configuration files.
    
- **Key Line** (Line 12):
    
    ```
    import init.zygote64.rc
    ```
    

### **2.** `**init.zygote64.rc**`

- **Purpose**: Configures the Zygote process for ARM64 systems.
    
- **Command to Start Zygote**:
    
    ```
    service zygote /system/bin/app_process64 -Xzygote /system/bin --zygote --start-system-server --socket-name=zygote
    ```
    

### **3. Code Reference in AOSP**

- Path: `app_main.cpp` (Referenced via `app_process64`).
    
- Starts the **main() function**, which processes arguments and sets up the runtime environment.
    

---

## 5. System Server and Zygote Process Forking

- **System Server**:
    
    - Launched using the `--start-system-server` flag.
        
    - Critical for managing core system services.
        
- **Forking Mechanism**:
    
    - Zygote employs the `fork()` system call to create child processes efficiently.
        
- **Why Forking Works Well**:
    
    - The parent Zygote process is initialized with:
        
        - Android Runtime (ART/Dalvik)
            
        - Core system libraries and resources
            
    - Child processes inherit these resources without reloading them.
        
    - This reduces:
        
        - Process startup time
            
        - Memory consumption through shared memory.
            
- **Steps**:
    
    1. Zygote process forks a child.
        
    2. Child inherits the Android Runtime (ART/Dalvik).
        
    3. System Server or application processes are initialized.
        

### Code Analysis for Forking:

- Found in `app_main.cpp`:
    
    - Key Functionality:
        
        - Parses command-line arguments.
            
        - Sets the `start-system-server` flag to `true`.
            
    - Invokes the `ZygoteInit` process in Java to handle further actions.
        

---

## 6. Code Analysis and Key Paths

### Key Files in AOSP Codebase:

|File|Path/Reference|Role|
|---|---|---|
|`**init.cpp**`|Android Source Code|Initializes boot scripts, references `init.rc`.|
|`**app_main.cpp**`|Core AOSP File|Main function that sets up Zygote and System Server.|
|`**AndroidRuntime**`|`frameworks/base/core/jni/`|Starts the Android Runtime.|
|`**zygoteinit.java**`|Android Java Layer|Entry point for Zygote process, handles process forking.|
|`**zygoteServer.java**`|Java Class|Handles continuous requests to spawn child processes.|

### Function Summary:

1. **Main Function** (`app_main.cpp`): Processes Zygote arguments.
    
2. **AndroidRuntime**: Starts the Android runtime.
    
3. **ZygoteInit** (`zygoteinit.java`):
    
    - Parses arguments.
        
    - Forks the **System Server**.
        
    - Enters a **select loop** to listen for new application launch requests.
        
4. **ZygoteServer**: Infinite loop for receiving connections and spawning processes.
    

---

## 7. Drawbacks: ASLR Limitations

- **Address Space Layout Randomization (ASLR)**:
    
    - ASLR ensures processes have random memory layouts for security.
        
    - However, since Zygote uses the **forking mechanism**, child processes inherit the memory layout.
        

### Why ASLR is Compromised with Forking:

- The Zygote process preloads shared libraries and initializes memory before forking.
    
- When a child process is created, it inherits this identical memory layout.
    
- This predictable memory layout can be exploited by attackers to bypass ASLR protections.
    

### Demonstration of ASLR Weakness:

1. Use `ADB` to find memory mappings:
    
    ```
    adb shell
    find / -iname libc.so
    cat /proc/<pid>/maps | grep r-x | cut -d' ' -f1 | sort | uniq
    ```
    
2. Observation:
    
    - **Repetitions** in addresses indicate lack of ASLR for Zygote child processes.