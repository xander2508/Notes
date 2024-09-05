`Onesixtyone` can be used to brute-force the names of the community strings since they can be named arbitrarily by the administrator. Since these community strings can be bound to any source, identifying the existing community strings can take quite some time.

[onesixtyone | Kali Linux Tools](https://www.kali.org/tools/onesixtyone/)

## Usage 

Wordlists: [[1. Wordlist Guide#SNMP Community Strings|SNMP Community Strings]]

```shell-session
onesixtyone -c /opt/useful/SecLists/Discovery/SNMP/snmp.txt 10.129.14.128
```

```
Scanning 1 hosts, 3219 communities
10.129.202.20 [backup] Linux NIXHARD 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64
```