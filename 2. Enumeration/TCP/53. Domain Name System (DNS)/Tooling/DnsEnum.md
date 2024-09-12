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

Wordlist: [[1. Wordlist and Password Guide#DNS Enumeration|DNS Enumeration]]

# Usage

```
dnsenum --threads 64 --dnsserver 10.10.10.224 -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt realcorp.htb
```

```shell-session
dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb
```

```shell-session
┌─[us-academy-1]─[10.10.14.69]─[htb-ac413848@pwnbox-base]─[~]
└──╼ [★]$ dnsenum --dnsserver 10.129.42.195 --enum -p 0 -s 0 -f /usr/share/SecLists/Discovery/DNS/namelist.txt dev.inlanefreight.htb

dnsenum VERSION:1.2.6

<SNIP>

Brute forcing with /usr/share/SecLists/Discovery/DNS/namelist.txt:
___________________________________________________________________

dev1.dev.inlanefreight.htb.              604800   IN    A         10.12.3.6
ns.dev.inlanefreight.htb.                604800   IN    A         127.0.0.1
win2k.dev.inlanefreight.htb.             604800   IN    A        10.12.3.203

<SNIP>
```