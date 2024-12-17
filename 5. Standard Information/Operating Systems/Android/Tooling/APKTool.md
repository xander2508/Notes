APK reverse engineering involves analyzing, decompiling, and modifying APK files. By doing so, we can study an application's inner workings, identify vulnerabilities, and alter its behavior.

### Key Tools

- **APK Tool**: A powerful utility for:
    - Decompiling APK files into human-readable formats.
    - Modifying code, resources, and rebuilding APKs.
    - Decoding Android resources like `AndroidManifest.xml`, layouts, images, and strings.
### Workflow:

1. **Decompiling APK Files**:
    
    - Use the command:
        
        ```
        apktool d <apk_file> -o <output_folder>
        ```
        
        - `d` stands for decompile.
            
        - `-o` specifies the output folder for decompiled files.
            
2. **Inspecting Decompiled Files**:
    
    - Key files include:
        
        - `AndroidManifest.xml`: Lists package names, permissions, activities, services, and receivers.
            
        - `res/`: Contains resource files like layouts, strings, and images.
            
        - `smali/`: Contains Smali code, the human-readable version of Dalvik bytecode.
            
3. **Rebuilding the APK**:
    
    - After modifications, rebuild the APK using:
        
        ```
        apktool b <output_folder>
        ```
        
4. **Analyzing Smali Code**:
    
    - Smali is an intermediate representation of Android bytecode.
        
    - Acts as a low-level representation akin to assembly language.

## APK Decompilation Example

1. **Decompile APK**:
    
    - Run:
        
        ```
        apktool d sarah.apk -o output
        ```
        
    - Outputs files into the `output/` folder.
        
2. **Key Findings in** `**AndroidManifest.xml**`:
    
    - Package Name: `turex.hackers.id`
        
    - Build Version: 29, Platform Version: 10.
        
    - **Permissions**:
        
        - Example: `android.permission.RECEIVE_BOOT_COMPLETED`.
            
    - **Debug Flag**:
        
        - Debug mode is enabled (`android:debuggable="true"`).
            
    - **Activities**:
        
        - The entry point is determined using:
            
            ```
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
            ```
            
    - **Services and Receivers**:
        
        - Example: `BootReceiver` with permission `RECEIVE_BOOT_COMPLETED`.
            
3. **Inspect Resource Files**:
    
    - `res/layout/`: Layout files like `main.xml`.
        
    - `res/values/strings.xml`: Example string: "Make BTC payment".
        
4. **Smali Folder**:
    
    - Smali files are found under `smali/com/turex/hackers/id/MainActivity.smali`.
        
    - Represents human-readable Dalvik bytecode.
        


See [[Smali]]