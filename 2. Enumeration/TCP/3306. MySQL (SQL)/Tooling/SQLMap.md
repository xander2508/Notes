---
tags:
  - Enumeration
  - TCP
---
SQLMap is an open-source penetration testing tool that automates the process of detecting and exploiting SQL injection vulnerabilities in web applications.

[GitHub - sqlmapproject/sqlmap: Automatic SQL injection and database takeover tool](https://github.com/sqlmapproject/sqlmap/tree/master)
# Options

- `—-dump`: Dump DBMS database table entries
- `—-batch`: Never ask for user input, use the default behaviour

# Example

How to provide more information and strings which indicate failure.
Provides the HTTP query to be used.
```
sqlmap -level=5 -risk=3 -p username --string="Wrong identification" --dump --batch -r login-request.txt
```

```
sqlmap -r login.req --level 5 --risk 3 --batch
```
```
sqlmap -r r.txt --level 5 --risk 3 --technique=BEUSTQ --random-agent -p "limit" --tamper="space2comment.py" --flush-session --batch
```