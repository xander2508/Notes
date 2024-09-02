---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Information
---

We might not notice anything like fuzzing right away when analysing our web server's traffic. However, this does not always indicate that nothing bad is happening. Instead, we can always look a little bit deeper. In order to do so, we might look for strange behaviour among HTTP requests. Some of which are weird headers like

Suppose we noticed that this filter returned some results, we could dig into these HTTP requests a little deeper to find out what hosts these bad actors might have tried to use. We might commonly notice `127.0.0.1`. Or instead something like admin.

Attackers will attempt to use different host headers to gain levels of access they would not normally achieve through the legitimate host. They may use proxy tools like burp suite or others to modify these before sending them to the server. In order to prevent successful exploitation beyond only detecting these events, we should always do the following.

1. `Ensure that our virtualhosts or access configurations are setup correctly to prevent this form of access.`
2. `Ensure that our web server is up to date.`
 
## Analysing Code 400s and Request Smuggling

We might also notice some bad responses from our web server, like code 400s. These codes indicate a bad request from the client, so they can be a good place to start when detecting malicious actions via http/https. In order to filter for these, we can use the following
- `http.response.code == 400`


