---
tags:
  - Enumeration
  - TCP
  - SMTP
  - Tooling
  - SimpleMailTransferProtocol
---
Username guessing tool primarily for use against the default Solaris SMTP service. Can use either EXPN, VRFY or RCPT TO.

[smtp-user-enum | Kali Linux Tools](https://www.kali.org/tools/smtp-user-enum/)

## Usage

```shell-session
smtp-user-enum -M RCPT -U userlist.txt -D inlanefreight.htb -t 10.129.203.7
```