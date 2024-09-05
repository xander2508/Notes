---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Tooling
  - HyperTextTransferProtocol
---

[GitHub - EnableSecurity/wafw00f: WAFW00F allows one to identify and fingerprint Web Application Firewall (WAF) products protecting a website.](https://github.com/EnableSecurity/wafw00f)

To do its magic, WAFW00F does the following:

- Sends a _normal_ HTTP request and analyses the response; this identifies a number of WAF solutions.
- If that is not successful, it sends a number of (potentially malicious) HTTP requests and uses simple logic to deduce which WAF it is.
- If that is also not successful, it analyses the responses previously returned and uses another simple algorithm to guess if a WAF or security solution is actively responding to our attacks.

## Installation

```
pipx install git+https://github.com/EnableSecurity/wafw00f.git
```
or 
```shell-session
pip3 install git+https://github.com/EnableSecurity/wafw00f
```
## Usage

```
wafw00f https://example.org
```