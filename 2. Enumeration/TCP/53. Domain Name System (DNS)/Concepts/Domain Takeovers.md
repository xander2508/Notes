---
tags:
  - Enumeration
  - TCP
  - DNS
  - DomainNameSystem
  - Concepts
---
`Domain takeover` is registering a non-existent domain name to gain control over another domain. If attackers find an expired domain, they can claim that domain to perform further attacks such as hosting malicious content on a website or sending a phishing email leveraging the claimed domain.

Domain takeover is also possible with subdomains called `subdomain takeover`. A DNS's canonical name (`CNAME`) record is used to map different domains to a parent domain. Many organizations use third-party services like AWS, GitHub, Akamai, Fastly, and other content delivery networks (CDNs) to host their content. In this case, they usually create a subdomain and make it point to those services. For example:

```shell-session
sub.target.com.   60   IN   CNAME   anotherdomain.com
```

The domain name (e.g., `sub.target.com`) uses a CNAME record to another domain (e.g., `anotherdomain.com`). Suppose the `anotherdomain.com` expires and is available for anyone to claim the domain since the `target.com`'s DNS server has the `CNAME` record. In that case, anyone who registers `anotherdomain.com` will have complete control over `sub.target.com` until the DNS record is updated.



