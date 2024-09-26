---
tags:
  - Enumeration
  - TCP
  - SMTP
  - SimpleMailTransferProtocol
  - Concepts
  - Information
---

See [[2. Enumeration/TCP/25. Simple Mail Transfer Protocol (SMTP)/2. Information#Open Relay Configuration|Information]]

An open relay is a Simple Mail Transfer Protocol (`SMTP`) server, which is improperly configured and allows an unauthenticated email relay. Messaging servers that are accidentally or intentionally configured as open relays allow mail from any source to be transparently re-routed through the open relay server. This behaviour masks the source of the messages and makes it look like the mail originated from the open relay server.

From an attacker's standpoint, we can abuse this for phishing by sending emails as non-existing users or spoofing someone else's email. For example, imagine we are targeting an enterprise with an open relay mail server, and we identify they use a specific email address to send notifications to their employees. We can send a similar email using the same address and add our phishing link with this information. With the `nmap smtp-open-relay` script, we can identify if an SMTP port allows an open relay.

```shell-session
nmap -p25 -Pn --script smtp-open-relay 10.10.11.213
```

Next, we can use any mail client to connect to the mail server and send our email.

```shell-session
swaks --from notifications@inlanefreight.com --to employees@inlanefreight.com --header 'Subject: Company Notification' --body 'Hi All, we want to hear from you! Please complete the following survey. http://mycustomphishinglink.com/' --server 10.10.11.213
```