---
tags:
  - Enumeration
  - TCP
  - DNS
  - DomainNameSystem
  - Tooling
---
Multithreaded Perl script to enumerate DNS information of a domain and to discover non-contiguous IP blocks.

[GitHub - fwaeytens/DnsEnum: DnsEnum is a Perl script that enumerates DNS information](https://github.com/fwaeytens/dnsenum)

Wordlist: [[1. Wordlist Guide#DNS Enumeration|DNS Enumeration]]

# Usage

```
dnsenum --threads 64 --dnsserver 10.10.10.224 -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt realcorp.htb
```

```shell-session
dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb
```