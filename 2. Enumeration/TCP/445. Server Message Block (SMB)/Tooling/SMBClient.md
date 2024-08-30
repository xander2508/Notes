---
tags:
  - Enumeration
  - TCP
  - Server-Message-Block
  - SMB
  - Tooling
---

# Guide

1. Can be used to traverse or log into new users, `smbclient -L //<IP> -U <USER>`
# Examples

List available shares:

```
smbclient --list //arkham.htb/ -U ""
```

```
smbclient -L 10.10.10.59 -U XXXXX
```

```
smbclient --list //sizzle.htb/ -U ""
```

Connect using NT hash:
```
smbclient //sizzle.htb/C$ -U "Administrator" --pw-nt-hash f6b7160bfc91823792e0ac3a162c9267
```