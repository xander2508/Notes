## Introduction to Simplify

- **Simplify** is a critical tool for reverse engineering obfuscated Android binaries.
- It uses **Smiley VM**, a virtual machine that acts as a sandbox, to:
    - Execute all possible execution paths for each function.
    - Generate context-sensitive graphs for methods based on execution paths.
- Key Features:
    - Identifies and removes dead code.
    - Performs constant propagation, reflection analysis, and peephole optimizations.
- **Tool Setup**:
    - Requires a compiled Simplify JAR binary.
    - Command to use: `java -jar simplify.jar`.

## Basic Operations

### Accessing Simplify's Features

- Use the `-h` or `--help` flag to view options.
- **`-it` (include types)**:
    - Specifies code portions to target using regex.

### Example: Viewing an Obfuscated Binary

1. Load the APK in a decompiler like JDX GUI.
2. Analyze specific classes (e.g., `reflection` class) for obfuscation patterns such as:
    - Use of `Class.forName`.
    - Obfuscation through redundant code or reflection APIs.

## Using Simplify

### Full Package Obfuscation

1. Identify the target package name (e.g., `org.cf.obfuscated`).
2. Format the package name for regex (replace dots with slashes).
3. Run: `java -jar simplify.jar -it org/cf/obfuscated path/to/app.apk`.
4. Handle errors such as incompatible Java versions by:
    - Using Java 8 instead of newer versions.
    - Updating the environment path to point to Java 8.

### Specific Class Obfuscation

1. Specify the target class in addition to the package (e.g., `org/cf/obfuscated/reflection`).
2. Command: `java -jar simplify.jar -it org/cf/obfuscated/reflection path/to/app.apk`.

### Function-Specific Obfuscation

1. Add the function name in **Smiley format**:
    - Example: `org/cf/obfuscated/reflection;->reflectSecretMethod`.
2. Run: `java -jar simplify.jar -it org/cf/obfuscated/reflection;->reflectSecretMethod path/to/app.apk`.

### Excluding Specific Classes

- Use **`-et` (exclude types)**:
    - Example: Exclude `MainActivity` to reduce analysis time.
    - Command: `java -jar simplify.jar -et MainActivity path/to/app.apk`.

## Optimization Tips

- **Address Warnings**: Use flags like `--max-address-visits` and `--max-call-depth` to handle execution path errors.
- **Targeted Analysis**:
    - Specific classes or functions save time compared to analyzing the entire package.
    - Efficient for obfuscated malware binaries.

## Outputs and Validation

- Simplify generates a new **unobfuscated binary** with a `.simplified` postfix.
- Load the new APK in tools like JDX GUI to verify:
    - Previously obfuscated code (e.g., reflection API usage) should now appear simplified.
    - Static analysis tools can now process the APK without breaking.

## Summary

- Simplify effectively removes obfuscation from APK and DEX files, making reverse engineering easier.
- It allows fine-tuned analysis of entire packages, specific classes, or functions.
- Java version compatibility and targeted use improve efficiency and reduce runtime.
- The tool enables additional static analysis tools to function seamlessly on the processed binaries.