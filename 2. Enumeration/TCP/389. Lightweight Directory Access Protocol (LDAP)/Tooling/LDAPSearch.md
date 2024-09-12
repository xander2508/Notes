---
tags:
  - Enumeration
  - TCP
  - LightweightDirectoryAccessProtocol
  - LDAP
  - Tooling
---

```
ldapsearch -LLL -x -H ldap://192.168.240.122 -b '' -s base '(objectclass=*)'
```

```
ldapsearch -h 192.168.240.122 -x -s base namingcontexts
```

```
ldapsearch -x -h 192.168.89.122 -D '' -w '' -b "DC=hutch,DC=offsec"
```

```
ldapsearch -x -h 192.168.102.122 -D 'hutch\fmcsorley' -w 'CrabSharkJellyfish192' -b 'dc=hutch,dc=offsec' "(ms-MCS-AdmPwd=*)" ms-MCS-AdmPwd
```

```
 ldapsearch -v -x -b "DC=hutch,DC=offsec" -H "ldap://192.168.120.108" "(objectclass=*)"
```