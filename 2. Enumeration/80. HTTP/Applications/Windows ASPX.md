
- ASPX pages are the primary building blocks of a Windows ASP.NET application.
- These pages contain server-side code written in languages like C# or VB.NET within special <% %> tags.
- ASPX pages are processed on the server before being sent to the client's browser, allowing for dynamic content generation.
- The use of ASPX pages allows for the creation of interactive web applications with rich functionality.
- Windows ASPX provides a robust framework for building secure and scalable web applications.

# Remote Code Execution

An ASPX shell comes with Kali Linux.
## File Upload

### Guide

[HTB: Bounty | 0xdf hacks stuff](https://0xdf.gitlab.io/2018/10/27/htb-bounty.html#transferaspx--uploadedfiles)

1. Check the `web.config` file as it has settings on the configuration data for the web application
2. Code within the `web.config` can potentially be executed
3. Upload a modified `web.config` file

For specific reverse shells, see [[Web Shells#ASPX]]
