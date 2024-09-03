---
tags:
  - Enumeration
  - TCP
  - SNMP
  - SimpleNetworkManagementProtocol
  - Tooling
---
`Snmpwalk` is used to query the OIDs with their information.

[SnmpWalk(1) - Linux man page](https://linux.die.net/man/1/snmpwalk)

# Guide

1. First install [[SNMP-MIBS-Downloader]]
# Walkthrough

1. [Hack The Box - Conceal - 0xRick’s Blog](https://0xrick.github.io/hack-the-box/conceal/)


# Example Commands 

```bash
snmpwalk -c public -v 1 conceal.htb
```

```shell-session
snmpwalk -v2c -c public 10.129.14.128
```