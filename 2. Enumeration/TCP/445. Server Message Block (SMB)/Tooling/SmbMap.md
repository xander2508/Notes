---
tags:
  - Enumeration
  - TCP
  - ServerMessageBlock
  - SMB
  - Tooling
---

[GitHub - ShawnDEvans/smbmap: SMBMap is a handy SMB enumeration tool](https://github.com/ShawnDEvans/smbmap)

## Usage

```shell-session
smbmap -H 10.129.14.128
```
### Using Credentials

```bash
smbmap -H 10.10.10.100 -u SVC_TGS -p GPPstillStandingStrong2k18
```

### Recursive List

```shell-session
smbmap -H 10.129.14.128 -r notes
```

### Download/Upload Files

```shell-session
smbmap -H 10.129.14.128 --download "notes\note.txt"
```

```shell-session
smbmap -H 10.129.14.128 --upload test.txt "notes\test.txt"
```






















