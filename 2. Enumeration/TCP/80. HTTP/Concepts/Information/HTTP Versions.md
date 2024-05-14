- HTTP/0.9: The first version of HTTP, introduced in 1991, was a simple protocol that allowed for transferring plain text data between a client and a server. It only supported the GET method and did not include headers or status codes.

- HTTP/1.0: This version, released in 1996, introduced several improvements such as support for different types of data, caching mechanisms, and the POST method. It also included headers for request and response metadata.

- HTTP/1.1: Released in 1999, this version is still widely used today. It added support for persistent connections, chunked transfer encoding, host headers, and more efficient caching mechanisms. It also introduced various optimizations to improve performance.

- HTTP/2: Introduced in 2015, this version aimed to address the limitations of HTTP/1.1 by optimizing the way data is transferred between clients and servers. It introduced features such as multiplexing, header compression, and server push to reduce latency and improve performance.

- HTTP/3: The latest version of HTTP is currently under development and is based on the QUIC protocol developed by Google. It aims to further improve performance by reducing latency through features such as encrypted connections by default and faster connection establishment.

Overall, the evolution of HTTP versions has been driven by the need to improve performance, security, and efficiency in transferring data over the internet. Each new version has built upon the previous one to address shortcomings and adapt to changing technologies and user needs.

# Guide

If a link has been found which appears dead, attempt a differing protocol to view the site, see [curl/docs/HTTP3.md at master · curl/curl · GitHub](https://github.com/curl/curl/blob/master/docs/HTTP3.md#quiche-version)

`curl --http3 https://portal.quick.htb/`

# Credentials Requirement

1. [Hack The Box - Sizzle - 0xRick’s Blog](https://0xrick.github.io/hack-the-box/sizzle/)

```
openssl req -newkey rsa:2048 -nodes -keyout request.key -out request.csr
```