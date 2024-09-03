---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Tooling
  - Fuzzing
  - HyperTextTransferProtocol
---
# User Agent

Apply the following to any command

```
--random-agent
```


# Commands 

```
gobuster dir -u http://192.168.89.84/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -e -k -s "200,204,301,302,307,403,500" -x "txt,html,php,asp,aspx,jsp"
```

```
gobuster dir -u http://192.168.190.138/ -w /usr/share/wordlists/dirb/big.txt -e -k -s "200,204,301,302,307,403,500" -x "txt,html,php,asp,aspx,jsp" 
```

```
gobuster dir -u http://192.168.190.138/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -e -k -s "200,204,301,302,307,403" -b "500" -x "txt,html,php,asp,aspx,jsp" --wildcard
```