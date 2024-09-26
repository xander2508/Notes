---
tags:
  - Enumeration
  - TCP
  - SMTP
  - Tooling
  - SimpleMailTransferProtocol
---

o365spray is a username enumeration and password spraying tool aimed at Microsoft Office 365 (O365).

[Fetching Title#91db](https://github.com/0xZDH/o365spray)

Validate a domain is using O365:  
```
o365spray --validate --domain test.com
```

Perform username enumeration against a given domain:  
```
o365spray --enum -U usernames.txt --domain test.com
```

Perform password spraying against a given domain:  
```
o365spray --spray -U usernames.txt -P passwords.txt --count 2 --lockout 5 --domain test.com
```