---
tags:
  - Enumeration
  - TCP
  - DNS
  - DomainNameSystem
  - Tooling
---

DNS reconnaissance and subdomain enumeration tool with recursive search and wildcard detection.	

[GitHub - mschwager/fierce: A DNS reconnaissance tool for locating non-contiguous IP space.](https://github.com/mschwager/fierce)

## Installation

```
$ python -m pip install fierce
$ fierce -h
```

## Usage

```
 fierce --domain google.com --subdomains accounts admin ads
```

```
fierce --domain zonetransfer.me
```

##### Internal Networks 

```
fierce --dns-servers 10.0.0.1 --range 10.0.0.0/24
```