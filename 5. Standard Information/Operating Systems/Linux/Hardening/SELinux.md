---
tags:
  - OperatingSystems
  - Linux
  - Hardening
  - StandardInformation
---
SELinux is a MAC system that is built into the Linux kernel. It is designed to provide fine-grained access control over system resources and applications. SELinux works by enforcing a policy that defines the access controls for each process and file on the system. It provides a higher level of security by limiting the damage that a compromised process can do.

 In SELinux, every process, file, directory, and system object is given a label. Policy rules are created to control access between these labelled processes and objects and are enforced by the kernel. This means that access can be set up to control which users and applications can access which resources. SELinux provides very granular access controls, such as specifying who can append to a file or move it.