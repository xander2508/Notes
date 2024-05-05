


# Password Cracking

* [[Hydra#WordPress]]

# Scanning

```bash
wpscan --url "http://192.168.51.28" -e ap,at,cb,dbe,u --plugins-detection aggressive --api-token FFecATFWJkJRJscMHLXiSKx5PGgWcbj6iOiQgsvsnIM
```

```bash
wpscan --url "http://192.168.51.28" -e u -P /usr/share/seclists/Passwords/Common-Credentials/500-worst-passwords.txt
```

```bash
wpscan --url tenten.htb --enumerate ap,at,cb,dbe --plugins-detection aggressive
```