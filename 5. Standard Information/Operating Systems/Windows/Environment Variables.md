Environment variables are settings that are often applied globally to our hosts. On a Windows host, environment variables are `not` case sensitive and can have spaces and numbers in the name. The only real catch we will find is that they cannot have a name that starts with a number or include an equal sign. When referenced, we will see these variables called like so:

```cmd-session
%SUPER_IMPORTANT_VARIABLE%
```

#### Variable Scopes

In this context, `Scope` is a programming concept that refers to where variables can be accessed or referenced. 'Scope' can be broadly separated into two categories:

- **Global:**
    - Global variables are accessible `globally`. In this context, the global scope lets us know that we can access and reference the data stored inside the variable from anywhere within a program.
- **Local:**
    - Local variables are only accessible within a `local` context. `Local` means that the data stored within these variables can only be accessed and referenced within the function or context in which it has been declared.

|Scope|Description|Permissions Required to Access|Registry Location|
|---|---|---|---|
|`System (Machine)`|The System scope contains environment variables defined by the Operating System (OS) and are accessible globally by all users and accounts that log on to the system. The OS requires these variables to function properly and are loaded upon runtime.|Local Administrator or Domain Administrator|`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment`|
|`User`|The User scope contains environment variables defined by the currently active user and are only accessible to them, not other users who can log on to the same system.|Current Active User, Local Administrator, or Domain Administrator|`HKEY_CURRENT_USER\Environment`|
|`Process`|The Process scope contains environment variables that are defined and accessible in the context of the currently running process. Due to their transient nature, their lifetime only lasts for the currently running process in which they were initially defined. They also inherit variables from the System/User Scopes and the parent process that spawns it (only if it is a child process).|Current Child Process, Parent Process, or Current Active User|`None (Stored in Process Memory)`|

# Displaying Environment Variables 

#### Display with Set

```cmd-session
C:\Users\htb\Desktop>set %SYSTEMROOT%

Environment variable C:\Windows not defined
```

#### Display with Echo

```cmd-session
C:\Users\htb\>echo %PATH%

C:\Users\htb\Desktop
```

# Managing Environment Variables
We can either use `set` or `setx` to perform our intended actions.
The `set` utility only manipulates environment variables in the current command line session.
The `setx` utility makes the appropriate changes to the registry, which will exist upon restart of our current command prompt session.


#### Using set

```cmd-session
C:\htb> set DCIP=172.16.5.2
```

#### Validating the Change

```cmd-session
C:\htb> echo %DCIP%

172.16.5.2
```

#### Using setx

```cmd-session
C:\htb> setx DCIP 172.16.5.2

SUCCESS: Specified value was saved.
```

#### Removing Variables

This command will remove `%DCIP%` from our system's current environment variables and will also be reflected in the registry once we open a new command prompt session.

```cmd-session
C:\htb> setx DCIP ""
```


## Important Environment Variables

[Windows Environment Variables - Windows CMD - SS64.com](https://ss64.com/nt/syntax-variables.html)

|Variable Name|Description|
|---|---|
|`%PATH%`|Specifies a set of directories(locations) where executable programs are located.|
|`%OS%`|The current operating system on the user's workstation.|
|`%SYSTEMROOT%`|Expands to `C:\Windows`. A system-defined read-only variable containing the Windows system folder. Anything Windows considers important to its core functionality is found here, including important data, core system binaries, and configuration files.|
|`%LOGONSERVER%`|Provides us with the login server for the currently active user followed by the machine's hostname. We can use this information to know if a machine is joined to a domain or workgroup.|
|`%USERPROFILE%`|Provides us with the location of the currently active user's home directory. Expands to `C:\Users\{username}`.|
|`%ProgramFiles%`|Equivalent of `C:\Program Files`. This location is where all the programs are installed on an `x64` based system.|
|`%ProgramFiles(x86)%`|Equivalent of `C:\Program Files (x86)`. This location is where all 32-bit programs running under `WOW64` are installed. Note that this variable is only accessible on a 64-bit host. It can be used to indicate what kind of host we are interacting with. (`x86` vs. `x64` architecture)|
