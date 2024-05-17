
A Cross-Site Request Forgery (XSRF) is also known as “one-click attack” and “session riding”. The idea is that an attacker can craft a URL such that when a target visits it, some actions or commands are taken that the user may not have wanted to take. For a site that’s vulnerable to XSRF, this can be a nasty attack, since the attacker can control the text of the link they send the target, making it not too hard to trick people into clicking on links.

`CSRF` attacks may utilize [[Cross Site Scripting (XSS)]] vulnerabilities to perform certain queries, and `API` calls on a web application that the victim is currently authenticated to. This would allow the attacker to perform actions as the authenticated user. It may also utilize other vulnerabilities to perform the same functions, like utilizing HTTP parameters for attacks.

[HTB: SecNotes | 0xdf hacks stuff](https://0xdf.gitlab.io/2019/01/19/htb-secnotes.html)