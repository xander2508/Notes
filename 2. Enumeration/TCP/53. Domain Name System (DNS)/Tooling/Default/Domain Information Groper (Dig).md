
**dig** (domain information groper) is a flexible tool for interrogating DNS name servers. It performs DNS lookups and displays the answers that are returned from the name **server**(s) that were queried. Most DNS administrators use **dig** to troubleshoot DNS problems because of its flexibility, ease of use and clarity of output. Other lookup tools tend to have less functionality than **dig**.

Although **dig** is normally used with command-line arguments, it also has a batch mode of operation for reading lookup requests from a file. A brief summary of its command-line arguments and options is printed when the **-h** option is given. Unlike earlier versions, the BIND 9 implementation of **dig** allows multiple lookups to be issued from the command line.

Unless it is told to query a specific name server, **dig** will try each of the servers listed in `/etc/resolv.conf`.

When no command line arguments or options are given, **dig** will perform an NS query for "." (the root).

### Usage 

```shell-session
dig any inlanefreight.com
```

Reverse DNS query:

```
dig -x 10.129.1.203
```



1. Header
    
    - `;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16449`: This line indicates the type of query (`QUERY`), the successful status (`NOERROR`), and a unique identifier (`16449`) for this specific query.
        
        - `;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0`: This describes the flags in the DNS header:
            - `qr`: Query Response flag - indicates this is a response.
            - `rd`: Recursion Desired flag - means recursion was requested.
            - `ad`: Authentic Data flag - means the resolver considers the data authentic.
            - The remaining numbers indicate the number of entries in each section of the DNS response: 1 question, 1 answer, 0 authority records, and 0 additional records.
    - `;; WARNING: recursion requested but not available`: This indicates that recursion was requested, but the server does not support it.
        
2. Question Section
    
    - `;google.com. IN A`: This line specifies the question: "What is the IPv4 address (A record) for `google.com`?"
3. Answer Section
    
    - `google.com. 0 IN A 142.251.47.142`: This is the answer to the query. It indicates that the IP address associated with `google.com` is `142.251.47.142`. The '`0`' represents the `TTL` (time-to-live), indicating how long the result can be cached before being refreshed.
4. Footer
    
    - `;; Query time: 0 msec`: This shows the time it took for the query to be processed and the response to be received (0 milliseconds).
        
    - `;; SERVER: 172.23.176.1#53(172.23.176.1) (UDP)`: This identifies the DNS server that provided the answer and the protocol used (UDP).
        
    - `;; WHEN: Thu Jun 13 10:45:58 SAST 2024`: This is the timestamp of when the query was made.
        
    - `;; MSG SIZE rcvd: 54`: This indicates the size of the DNS message received (54 bytes).
        

An `opt pseudosection` can sometimes exist in a `dig` query. This is due to Extension Mechanisms for DNS (`EDNS`), which allows for additional features such as larger message sizes and DNS Security Extensions (`DNSSEC`) support.

If you just want the answer to the question, without any of the other information, you can query `dig` using `+short`:

```shell-session
dig +short hackthebox.com
```