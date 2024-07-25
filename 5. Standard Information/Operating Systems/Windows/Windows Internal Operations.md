
Windows operating systems function in two main modes:

- `User Mode`: This mode is where most applications and user processes operate. Applications in user mode have limited access to system resources and must interact with the operating system through Application Programming Interfaces (APIs). These processes are isolated from each other and cannot directly access hardware or critical system functions.
- `Kernel Mode`: In contrast, kernel mode is a highly privileged mode where the Windows kernel runs. The kernel has unrestricted access to system resources, hardware, and critical functions. It provides core operating system services, manages system resources, and enforces security and stability. Device drivers, which facilitate communication with hardware devices, also run in kernel mode.

![[windows_architecture.webp]]

### User-mode Components

`User-mode components` are those parts of the operating system that don't have direct access to hardware or kernel data structures. They interact with system resources through APIs and system calls. Let's discuss some of them:

- `System Support Processes`: These are essential components that provide crucial functionalities and services such as logon processes (`winlogon.exe`), Session Manager (`smss.exe`), and Service Control Manager (`services.exe`). These aren't Windows services but they are necessary for the proper functioning of the system.
- `Service Processes`: These processes host Windows services like the `Windows Update Service`, `Task Scheduler`, and `Print Spooler` services. They usually run in the background, executing tasks according to their configuration and parameters.
- `User Applications`: These are the processes created by user programs, including both 32-bit and 64-bit applications. They interact with the operating system through [APIs](https://en.wikipedia.org/wiki/Windows_API) provided by Windows. These API calls get redirected to [NTDLL.DLL](https://en.wikipedia.org/wiki/Microsoft_Windows_library_files#NTDLL.DLL), triggering a transition from user mode to kernel mode, where the system call gets executed. The result is then returned to the user-mode application, and a transition back to user mode occurs.
- `Environment Subsystems`: These components are responsible for providing execution environments for specific types of applications or processes. They include the [Win32 Subsystem](https://en.wikipedia.org/wiki/Architecture_of_Windows_NT#Win32_environment_subsystem), [POSIX](https://en.wikipedia.org/wiki/Microsoft_POSIX_subsystem), and [OS/2](https://en.wikipedia.org/wiki/OS/2).
- `Subsystem DLLs`: These dynamic-link libraries translate documented functions into appropriate internal native system calls, primarily implemented in `NTDLL.DLL`. Examples include `kernelbase.dll`, `user32.dll`, `wininet.dll`, and `advapi32.dll`.