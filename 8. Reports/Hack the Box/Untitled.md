PORT    STATE         SERVICE  VERSION
22/tcp  open          ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 3f:4c:8f:10:f1:ae:be:cd:31:24:7c:a1:4e:ab:84:6d (RSA)
|   256 7b:30:37:67:50:b9:ad:91:c0:8f:f7:02:78:3b:7c:02 (ECDSA)
|_  256 88:9e:0e:07:fe:ca:d0:5c:60:ab:cf:10:99:cd:6c:a7 (ED25519)
110/tcp open          pop3     Dovecot pop3d
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_pop3-capabilities: PIPELINING STLS USER UIDL TOP CAPA SASL(PLAIN) RESP-CODES AUTH-RESP-CODE
|_ssl-date: TLS randomness does not represent time
143/tcp open          imap     Dovecot imapd (Ubuntu)
|_imap-capabilities: capabilities ID IMAP4rev1 STARTTLS LOGIN-REFERRALS more have post-login ENABLE LITERAL+ listed Pre-login IDLE AUTH=PLAINA0001 OK SASL-IR
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_ssl-date: TLS randomness does not represent time
993/tcp open          ssl/imap Dovecot imapd (Ubuntu)
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: capabilities ID IMAP4rev1 Pre-login LOGIN-REFERRALS more have ENABLE LITERAL+ post-login listed IDLE AUTH=PLAINA0001 OK SASL-IR
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
995/tcp open          ssl/pop3 Dovecot pop3d
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_pop3-capabilities: TOP PIPELINING CAPA UIDL USER SASL(PLAIN) AUTH-RESP-CODE RESP-CODES
68/udp  open|filtered dhcpc
161/udp open          snmp     net-snmp; net-snmp SNMPv3 server
| snmp-info: 
|   enterprise: net-snmp
|   engineIDFormat: unknown
|   engineIDData: 5b99e75a10288b6100000000
|   snmpEngineBoots: 10
|_  snmpEngineTime: 47m02s
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
