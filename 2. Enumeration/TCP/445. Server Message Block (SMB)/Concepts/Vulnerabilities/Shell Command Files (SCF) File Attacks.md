---
tags:
  - Enumeration
  - TCP
  - ServerMessageBlock
  - SMB
  - Concepts
  - Vulnerabilities
---

Shell Command Files (SCF) are script files used by the Windows operating system to automate tasks through command line commands.
These files have a `.scf` file extension and can be executed by simply double-clicking on them.

- Malicious SCF files can be used in various types of attacks, including:
   a. Phishing attacks: Attackers can create SCF files that appear as harmless shortcuts but actually execute malicious commands when opened.
   b. Remote code execution: Attackers can embed malicious code in SCF files to remotely execute commands on a victim's system.
   c. Credential theft: SCF files can be used to harvest sensitive information such as usernames and passwords from unsuspecting users.


# Guide 

1. If you can get a user to click on a file, provide them a SCF file with a remote file path, then capture the users credentials using [[1. Recon/Tooling/Responder|Responder]]

# Walkthrough

1. [SMB Share – SCF File Attacks – Penetration Testing Lab](https://pentestlab.blog/2017/12/13/smb-share-scf-file-attacks/)
2. [Hack The Box - Sizzle - 0xRick’s Blog](https://0xrick.github.io/hack-the-box/sizzle/)