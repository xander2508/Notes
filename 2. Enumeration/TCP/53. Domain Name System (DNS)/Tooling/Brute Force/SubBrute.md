---
tags:
  - Enumeration
  - TCP
  - DNS
  - DomainNameSystem
  - Tooling
  - BruteForce
---

[GitHub - TheRook/subbrute: A DNS meta-query spider that enumerates DNS records, and subdomains.](https://github.com/TheRook/subbrute)

SubBrute is a community driven project with the goal of creating the fastest, and most accurate subdomain enumeration tool.

This tool allows us to use self-defined resolvers and perform pure DNS brute-forcing attacks during internal penetration tests on hosts that do not have Internet access.

## Installation

```shell-session
git clone https://github.com/TheRook/subbrute.git >> /dev/null 2>&1
```

```shell-session
cd subbrute
```

## Usage 

```shell-session
echo "ns1.inlanefreight.com" > ./resolvers.txt
```

```shell-session
./subbrute inlanefreight.com -s ./names.txt -r ./resolvers.txt
```