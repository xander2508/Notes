---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Vulnerabilities
  - HyperTextTransferProtocol
---

SSI (Server-Side Includes) is a simple scripting language used on web servers to include the contents of one file within another file. This allows for easy reusability of code and can help streamline the development process.

One of the key features of SSI is the ability to use "starred blocks" to define specific sections of a file that can be included or excluded based on certain conditions. Starred blocks are denoted by <!--#if expr="condition" --> and <!--#endif --> tags, with the condition determining whether the block should be included or not.

For example, a common use case for starred blocks is to display different content based on the user's login status. By using SSI to include different sections of a page based on whether the user is logged in or not, developers can create more personalized and dynamic web experiences.

Overall, starred blocks in SSI provide a powerful tool for developers to create dynamic and flexible web pages that can adapt based on user interactions or other conditions. By using SSI effectively, developers can enhance the functionality and usability of their websites while maintaining clean and organized code.
# Guide

1. [Server-Side Includes (SSI) Injection | OWASP Foundation](https://owasp.org/www-community/attacks/Server-Side_Includes_(SSI)_Injection)