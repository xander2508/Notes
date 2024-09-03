---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Information
  - HyperTextTransferProtocol
---
An important concept to learn in HTML is [URL Encoding](https://en.wikipedia.org/wiki/Percent-encoding), or percent-encoding. For a browser to properly display a page's contents, it has to know the charset in use. In URLs, for example, browsers can only use [ASCII](https://en.wikipedia.org/wiki/ASCII) encoding, which only allows alphanumerical characters and certain special characters. Therefore, all other characters outside of the ASCII character-set have to be encoded within a URL. URL encoding replaces unsafe ASCII characters with a `%` symbol followed by two hexadecimal digits.

|Character|Encoding|
|---|---|
|space|%20|
|!|%21|
|"|%22|
|#|%23|
|$|%24|
|%|%25|
|&|%26|
|'|%27|
|(|%28|
|)|%29|
A full character encoding table can be seen [here](https://www.w3schools.com/tags/ref_urlencode.ASP). Vulnerabilities 