---
tags:
  - Concepts
  - Vulnerabilities
  - Enumeration
  - TCP
  - DNS
  - DomainNameSystem
---
Read the `/etc/exports` file, if you find some directory that is configured as `no_root_squash`, then you can access it from as a client and write inside that directory as if you were the local **root** of the machine.

**no_root_squash**: This option basically gives authority to the root user on the client to access files on the NFS server as root. And this can lead to serious security implications.

no_all_squash: This is similar to no_root_squash option but applies to non-root users. 

Imagine, you have a shell as nobody user; checked `/etc/exports` file; 
no_all_squash option is present; 
check `/etc/passwd` file;
emulate a non-root user; 
create a SUID file as that user (by mounting using NFS). 
Execute the SUID as nobody user and become different user.

[NFS no\_root\_squash/no\_all\_squash misconfiguration PE | HackTricks | HackTricks](https://book.hacktricks.xyz/linux-hardening/privilege-escalation/nfs-no_root_squash-misconfiguration-pe)
[Linux privilege escalation using weak NFS permissions](https://haiderm.com/linux-privilege-escalation-using-weak-nfs-permissions/)