---
tags:
  - OperatingSystems
  - Linux
---

The XServer is the user-side part of the `X Window System network protocol` (`X11` / `X`). The `X11` is a fixed system that consists of a collection of protocols and applications that allow us to call application windows on displays in a graphical user interface. X11 is predominant on Unix systems, but X servers are also available for other operating systems. Nowadays, the XServer is a part of almost every desktop installation of Ubuntu and its derivatives and does not need to be installed separately.

# X11 Security

X11 is not a secure protocol without suitable security measures since X11 communication is entirely unencrypted. A completely open X server lets anyone on the network read the contents of its windows, for example, and this goes unnoticed by the user sitting in front of it. Therefore, it is not even necessary to sniff the network. This standard X11 functionality is realized with simple X11 tools like `xwd` and `xgrabsc`.

# X11Forwarding and SSH

  Remote Desktop Protocols in Linux

```shell-session
cat /etc/ssh/sshd_config | grep X11Forwarding

X11Forwarding yes
```

With this we can start the application from our client with the following command:

```shell-session
ssh -X htb-student@10.129.23.11 /usr/bin/firefox
```