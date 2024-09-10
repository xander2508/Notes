---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Applications
  - HyperTextTransferProtocol
---

This application is used by network & system administrators to automate the process of configuring network appliances. One practical use case would be to use rConfig to remotely configure network interfaces with IP addressing information on multiple routers simultaneously. This tool saves admins time but, if compromised, could be used to pivot onto critical network devices that switch & route packets across the network. 

A malicious attacker could own the entire network through rConfig since it will likely have admin access to all the network appliances used to configure. As pentesters, finding a vulnerability in this application would be considered a very critical discovery.


## Versions 

### 3.9.6

[rconfig 3.9.6 - Arbitrary File Upload - PHP webapps Exploit](https://www.exploit-db.com/exploits/49783)

[rce.rb at master · rapid7/metasploit-framework · GitHub](https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/linux/http/rconfig_vendors_auth_file_upload_rce.rb)






