#### Purpose of Modifying Android Applications

- **In-depth Analysis**: Enables researchers to uncover security vulnerabilities by altering app logic.
- **Security Restriction Bypass**: Overcome barriers such as SSL pinning or jailbreak detection.
- **Behavior Tracing**: Modify an app's logic to better understand its input handling, aiding in the discovery of flaws like authentication issues or cryptographic misconfigurations.
#### Case Study: Unlock Me Application

1. **Installation and Initial Interaction**:
    
    - Command: `adb install -r -g -t unlockme.apk`
    - Launch via the device icon.
    - The app requires a PIN; incorrect entries prompt an alert, while the correct PIN leads to a "Congratulations" screen.
2. **Objective**:
    
    - Bypass PIN verification to access the next screen without the correct PIN.

---

#### Analysing the Application Code

1. **Tool Utilized**: [[Jadx]] (Java Decompiler)
    - Launch Command: `jdx-gui`
    - Load the `UnlockMe.apk` into the UI.
2. **Code Exploration**:
    - Search for the keyword **"wrong pin"** to locate relevant code sections.
    - Identify the logic verifying the PIN: The application checks if the entered PIN matches a value from the `getPin` function.
    - Investigation revealed that the `getPin` function resides in the native space, complicating direct access.

---

#### Code Modification

1. **Logic Flip**:
    
    - Change the condition to trigger the "success" screen even with incorrect PIN inputs.
    - Original Condition: `if(pin.getText().toString().equals(getPin()))`
    - Modified Condition: `if(!pin.getText().toString().equals(getPin()))`
2. **Tools Used**: [[APKTool]]
    
    - Decompile Command: `apktool d unlockme.apk -o UnlockMePatched`
    - This extracts the APK into a folder (`UnlockMePatched`) containing the SMALI source code.
3. **Editing SMALI Code**:
    
    - Search the extracted SMALI code for the keyword **"wrong pin"** to find the validation logic.
    - Locate the condition and update it:
        - Change `if-eqz` (if equals to zero) to `if-nez` (if not equals to zero).

---

#### Recompiling the Application

1. **Rebuild Command**: `apktool b UnlockMePatched -o UnlockMePatched.apk`
2. **Troubleshooting Errors**:
    - Errors often stem from outdated APKTool versions.
    - Recommended Solution: Update to the latest APKTool version (e.g., 2.9.0.3).