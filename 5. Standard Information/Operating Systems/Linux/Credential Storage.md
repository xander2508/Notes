---
tags:
  - OperatingSystems
  - Linux
  - StandardInformation
aliases:
  - Password Storage
  - Shadow File
---
One of the most commonly used and standard mechanisms is [Pluggable Authentication Modules](https://web.archive.org/web/20220622215926/http://www.linux-pam.org/Linux-PAM-html/Linux-PAM_SAG.html) (`PAM`). The modules used for this are called `pam_unix.so` or `pam_unix2.so` and are located in `/usr/lib/x86_x64-linux-gnu/security/` in Debian based distributions. These modules manage user information, authentication, sessions, current passwords, and old passwords. For example, if we want to change the password of our account on the Linux system with `passwd`, PAM is called, which takes the appropriate precautions and stores and handles the information accordingly.

The `pam_unix.so` standard module for management uses standardized API calls from the system libraries and files to update the account information. The standard files that are read, managed, and updated are `/etc/passwd` and `/etc/shadow`. PAM also has many other service modules, such as LDAP, mount, or Kerberos.

Linux-based systems handle everything in the form of a file. Accordingly, passwords are also stored encrypted in a file. This file is called the `shadow` file and is located in `/etc/shadow` and is part of the Linux user management system. In addition, these passwords are commonly stored in the form of `hashes`. 

See [Linux User Authentication Guide](https://tldp.org/HOWTO/pdf/User-Authentication-HOWTO.pdf) 
## Shadow File

```shell-session
cat /etc/shadow

...SNIP...
htb-student:$y$j9T$3QSBB6CbHEu...SNIP...f8Ms:18955:0:99999:7:::
```

The `/etc/shadow` file has a unique format in which the entries are entered and saved when new users are created.

| `htb-student:` | `$y$j9T$3QSBB6CbHEu...SNIP...f8Ms:` | `18955:`                | `0:`         | `99999:`     | `7:`                | `:`                    | `:`                  | `:`However, a few more files belong to the user management system of Linux. The other two files are `/etc/passwd` and `/etc/group`.However, a few more files belong to the user management system of Linux. The other two files are `/etc/passwd` and `/etc/group`. |
| -------------- | ----------------------------------- | ----------------------- | ------------ | ------------ | ------------------- | ---------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `<username>`:  | `<encrypted password>`:             | `<day of last change>`: | `<min age>`: | `<max age>`: | `<warning period>`: | `<inactivity period>`: | `<expiration date>`: | `<reserved field>`                                                                                                                                                                                                                                                  |

The encryption of the password in this file is formatted as follows:

| `$ <id>` | `$ <salt>` | `$ <hashed>`                  |
| -------- | ---------- | ----------------------------- |
| `$ y`    | `$ j9T`    | `$ 3QSBB6CbHEu...SNIP...f8Ms` |

The type (`id`) is the cryptographic hash method used to encrypt the password. Many different cryptographic hash methods were used in the past and are still used by some systems today.

| **ID**   | **Cryptographic Hash Algorithm**                                      |
| -------- | --------------------------------------------------------------------- |
| `$1$`    | [MD5](https://en.wikipedia.org/wiki/MD5)                              |
| `$2a$`   | [Blowfish](https://en.wikipedia.org/wiki/Blowfish_(cipher))           |
| `$5$`    | [SHA-256](https://en.wikipedia.org/wiki/SHA-2)                        |
| `$6$`    | [SHA-512](https://en.wikipedia.org/wiki/SHA-2)                        |
| `$sha1$` | [SHA1crypt](https://en.wikipedia.org/wiki/SHA-1)                      |
| `$y$`    | [Yescrypt](https://github.com/openwall/yescrypt)                      |
| `$gy$`   | [Gost-yescrypt](https://www.openwall.com/lists/yescrypt/2019/06/30/1) |
| `$7$`    | [Scrypt](https://en.wikipedia.org/wiki/Scrypt)                        |
However, a few more files belong to the user management system of Linux. The other two files are `/etc/passwd` and `/etc/group`.

In the past, the encrypted password was stored together with the username in the `/etc/passwd` file, but this was increasingly recognized as a security problem because the file can be viewed by all users on the system and must be readable. The `/etc/shadow` file can only be read by the user `root`.

## Passwd File

```shell-session
cat /etc/passwd

...SNIP...
htb-student:x:1000:1000:,,,:/home/htb-student:/bin/bash
```

| `htb-student:` | `x:`          | `1000:`  | `1000:`  | `,,,:`       | `/home/htb-student:` | `/bin/bash`                       |
| -------------- | ------------- | -------- | -------- | ------------ | -------------------- | --------------------------------- |
| `<username>:`  | `<password>:` | `<uid>:` | `<gid>:` | `<comment>:` | `<home directory>:`  | `<cmd executed after logging in>` |

Root without a password:

```shell-session
root::0:0:root:/root:/bin/bash
```

The `x` in the password field indicates that the encrypted password is in the `/etc/shadow` file. However, the redirection to the `/etc/shadow` file does not make the users on the system invulnerable because if the rights of this file are set incorrectly, the file can be manipulated so that the user `root` does not need to type a password to log in. 

Therefore, an empty field means that we can log in with the username without entering a password.

