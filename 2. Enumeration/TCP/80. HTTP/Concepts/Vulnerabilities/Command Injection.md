---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Vulnerabilities
---
Commands can be sent to the server either using a URL parameter or maybe a input box. 
1. Ensure a [[#Web Application Firewall (WAF)]] is not blocking the command by varying the data sent between valid and invalid, or just things that may be blocked.
2. Ensure that the machine has the program you are attempting to run installed, e.g. it may not have CURL
3. Bash restrictions may be applying which restrict the commands to run, see [[Command Line Restrictions]]
4. A list of potential inputs which may hint at the type of issue being encountered, see [Reflecting Techniques - PoCs and Polygloths CheatSheet | HackTricks | HackTricks](https://book.hacktricks.xyz/pentesting-web/pocs-and-polygloths-cheatsheet)