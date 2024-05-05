
[GitHub - epi052/feroxbuster: A fast, simple, recursive content discovery tool written in Rust.](https://github.com/epi052/feroxbuster)

# Example Commands 

```bash
feroxbuster --url http://192.168.149.145/  -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x "txt,html,php,asp,aspx,jsp"
```

```bash
feroxbuster --url http://192.168.33.114:9998/  -w /usr/share/wordlists/dirb/big.txt  -x "txt,html,php,asp,aspx,jsp" -t 200
```