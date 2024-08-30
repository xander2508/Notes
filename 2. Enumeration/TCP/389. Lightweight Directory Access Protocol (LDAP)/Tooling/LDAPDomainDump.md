---
tags:
  - Enumeration
  - TCP
  - Lightweight-Directory-Access-Protocol
  - LDAP
  - Tooling
---
In an Active Directory domain, a lot of interesting information can be retrieved via LDAP by any authenticated user (or machine). This makes LDAP an interesting protocol for gathering information in the recon phase of a penetration test of an internal network. A problem is that data from LDAP often is not available in an easy to read format.

LDAPDomainDump is a tool which aims to solve this problem, by collecting and parsing information available via LDAP and outputting it in a human readable HTML format, as well as machine readable JSON and CSV/TSV/greppable files.

[GitHub - dirkjanm/ldapdomaindump: Active Directory information dumper via LDAP](https://github.com/dirkjanm/ldapdomaindump)