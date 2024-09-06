---
tags:
  - Recon
  - OpenSourceIntelligence
  - OSINT
  - Tooling
---
A Python-based reconnaissance tool offering a range of modules for different tasks like SSL certificate checking, Whois information gathering, header analysis, and crawling. Its modular structure enables easy customisation for specific needs.

[GitHub - thewhiteh4t/FinalRecon: All In One Web Recon](https://github.com/thewhiteh4t/FinalRecon)

`FinalRecon` offers a wealth of recon information:

- `Header Information`: Reveals server details, technologies used, and potential security misconfigurations.
- `Whois Lookup`: Uncovers domain registration details, including registrant information and contact details.
- `SSL Certificate Information`: Examines the SSL/TLS certificate for validity, issuer, and other relevant details.
- `Crawler`:
    - HTML, CSS, JavaScript: Extracts links, resources, and potential vulnerabilities from these files.
    - Internal/External Links: Maps out the website's structure and identifies connections to other domains.
    - Images, robots.txt, sitemap.xml: Gathers information about allowed/disallowed crawling paths and website structure.
    - Links in JavaScript, Wayback Machine: Uncovers hidden links and historical website data.
- `DNS Enumeration`: Queries over 40 DNS record types, including DMARC records for email security assessment.
- `Subdomain Enumeration`: Leverages multiple data sources (crt.sh, AnubisDB, ThreatMiner, CertSpotter, Facebook API, VirusTotal API, Shodan API, BeVigil API) to discover subdomains.
- `Directory Enumeration`: Supports custom wordlists and file extensions to uncover hidden directories and files.
- `Wayback Machine`: Retrieves URLs from the last five years to analyse website changes and potential vulnerabilities.


## Installation

```shell-session
git clone https://github.com/thewhiteh4t/FinalRecon.git
```
```shell-session
cd FinalRecon
```
```shell-session
pip3 install -r requirements.txt
```
```shell-session
chmod +x ./finalrecon.py
```
```shell-session
./finalrecon.py --help
```

## Usage 

```shell-session
./finalrecon.py --headers --whois --url http://inlanefreight.com
```

| Option         | Argument | Description                                         |
| -------------- | -------- | --------------------------------------------------- |
| `-h`, `--help` |          | Show the help message and exit.                     |
| `--url`        | URL      | Specify the target URL.                             |
| `--headers`    |          | Retrieve header information for the target URL.     |
| `--sslinfo`    |          | Get SSL certificate information for the target URL. |
| `--whois`      |          | Perform a Whois lookup for the target domain.       |
| `--crawl`      |          | Crawl the target website.                           |
| `--dns`        |          | Perform DNS enumeration on the target domain.       |
| `--sub`        |          | Enumerate subdomains for the target domain.         |
| `--dir`        |          | Search for directories on the target website.       |
| `--wayback`    |          | Retrieve Wayback URLs for the target.               |
| `--ps`         |          | Perform a fast port scan on the target.             |
| `--full`       |          | Perform a full reconnaissance scan on the target.   |