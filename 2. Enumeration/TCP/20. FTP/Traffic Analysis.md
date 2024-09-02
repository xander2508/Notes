---
tags:
  - Enumeration
  - TCP
  - FTP
---

See [[1. Analysis Overview]]

Within [[Wireshark]]:

- `ftp.request.command` - Will show any commands sent across the ftp-control channel (port 21)
    - We can look for information like usernames and passwords with this filter. It can also show us filenames for anything requested.
    
- `ftp-data` - Will show any data transferred over the data channel ( port 20 )
    - If we filter on a conversation and utilize `ftp-data`, we can capture anything sent during the conversation. We can reconstruct anything transferred by placing the raw data back into a new file and naming it appropriately.