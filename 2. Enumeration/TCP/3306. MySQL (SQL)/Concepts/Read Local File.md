---
tags:
  - Enumeration
  - TCP
  - MySQL
  - SQL
  - Concepts
---

 By default a `MySQL` installation does not allow arbitrary file read, but if the correct settings are in place and with the appropriate privileges, we can read files using the following methods:

```shell-session
select LOAD_FILE("/etc/passwd");
```