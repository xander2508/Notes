
A Cross-Site Request Forgery (XSRF) is also known as “one-click attack” and “session riding”. The idea is that an attacker can craft a URL such that when a target visits it, some actions or commands are taken that the user may not have wanted to take. For a site that’s vulnerable to XSRF, this can be a nasty attack, since the attacker can control the text of the link they send the target, making it not too hard to trick people into clicking on links.

`CSRF` attacks may utilize [[Cross Site Scripting (XSS)]] vulnerabilities to perform certain queries, and `API` calls on a web application that the victim is currently authenticated to. This would allow the attacker to perform actions as the authenticated user. It may also utilize other vulnerabilities to perform the same functions, like utilizing HTTP parameters for attacks.

# Guide 

[Cross-Site Request Forgery Prevention - OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)
# Walkthrough

[HTB: SecNotes | 0xdf hacks stuff](https://0xdf.gitlab.io/2019/01/19/htb-secnotes.html)

## Prevention

Though there should be measures on the back end to detect and filter user input, it is also always important to filter and sanitize user input on the front end before it reaches the back end, and especially if this code may be displayed directly on the client-side without communicating with the back end. Two main controls must be applied when accepting user input:

|Type|Description|
|---|---|
|`Sanitization`|Removing special characters and non-standard characters from user input before displaying it or storing it.|
|`Validation`|Ensuring that submitted user input matches the expected format (i.e., submitted email matched email format)|