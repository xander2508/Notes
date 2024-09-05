PORT      STATE    SERVICE     VERSION
22/tcp    open     ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 3f:4c:8f:10:f1:ae:be:cd:31:24:7c:a1:4e:ab:84:6d (RSA)
|   256 7b:30:37:67:50:b9:ad:91:c0:8f:f7:02:78:3b:7c:02 (ECDSA)
|_  256 88:9e:0e:07:fe:ca:d0:5c:60:ab:cf:10:99:cd:6c:a7 (ED25519)
110/tcp   open     pop3        Dovecot pop3d
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_ssl-date: TLS randomness does not represent time
|_pop3-capabilities: STLS SASL(PLAIN) AUTH-RESP-CODE CAPA UIDL TOP RESP-CODES PIPELINING USER
143/tcp   open     imap        Dovecot imapd (Ubuntu)
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_imap-capabilities: more OK STARTTLS have AUTH=PLAINA0001 ENABLE LITERAL+ listed capabilities IDLE LOGIN-REFERRALS SASL-IR Pre-login post-login ID IMAP4rev1
|_ssl-date: TLS randomness does not represent time
993/tcp   open     ssl/imap    Dovecot imapd (Ubuntu)
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_ssl-date: TLS randomness does not represent time
|_imap-capabilities: OK more have LITERAL+ ENABLE AUTH=PLAINA0001 listed capabilities IDLE LOGIN-REFERRALS SASL-IR Pre-login post-login ID IMAP4rev1
995/tcp   open     ssl/pop3    Dovecot pop3d
| ssl-cert: Subject: commonName=NIXHARD
| Subject Alternative Name: DNS:NIXHARD
| Not valid before: 2021-11-10T01:30:25
|_Not valid after:  2031-11-08T01:30:25
|_ssl-date: TLS randomness does not represent time
|_pop3-capabilities: SASL(PLAIN) UIDL TOP RESP-CODES CAPA PIPELINING AUTH-RESP-CODE USER
1079/tcp  filtered asprovatalk
1130/tcp  filtered casp
5002/tcp  filtered rfe
8031/tcp  filtered unknown
49400/tcp filtered compaqdiag
