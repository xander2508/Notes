wFuzz is a powerful web application security testing tool that is designed to help test the security of web applications by fuzzing their parameters. Fuzzing is a technique used to find vulnerabilities in software by sending random or malformed data to the target application and observing its behavior.

wFuzz allows users to automate the process of fuzzing website parameters, making it easier to discover potential security flaws such as SQL injection, cross-site scripting, and more. It supports various types of payloads, including dictionaries, brute force, and predefined lists.

# Walkthrough

* [HTB: FluxCapacitor | 0xdf hacks stuff](https://0xdf.gitlab.io/2018/05/12/htb-fluxcapacitor.html)


# Fuzzing Sub-Domains

```
wfuzz -c -u http://10.10.10.186:9001 -H "Host: FUZZ.quick.htb" -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt --hh 3351
```

```
sudo wfuzz -c -f sub-fighter.txt -Z -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --sc 200,202,204,301,302,307,403 http://FUZZ.fritz.box
```