
Windows operating systems function in two main modes:

- `User Mode`: This mode is where most applications and user processes operate. Applications in user mode have limited access to system resources and must interact with the operating system through Application Programming Interfaces (APIs). These processes are isolated from each other and cannot directly access hardware or critical system functions.
- `Kernel Mode`: In contrast, kernel mode is a highly privileged mode where the Windows kernel runs. The kernel has unrestricted access to system resources, hardware, and critical functions. It provides core operating system services, manages system resources, and enforces security and stability. Device drivers, which facilitate communication with hardware devices, also run in kernel mode.

![[windows_architecture.webp]]

