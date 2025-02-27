---
tags:
  - Recon
  - PortScanning
  - Nmap
  - Tooling
---
 Nmap Scripting Engine (`NSE`) is a handy feature of `Nmap`. It provides us with the possibility to create scripts in Lua for interaction with certain services. There are a total of 14 categories into which these scripts can be divided:

| **Category** | **Description**                                                                                                                         |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `auth`       | Determination of authentication credentials.                                                                                            |
| `broadcast`  | Scripts, which are used for host discovery by broadcasting and the discovered hosts, can be automatically added to the remaining scans. |
| `brute`      | Executes scripts that try to log in to the respective service by brute-forcing with credentials.                                        |
| `default`    | Default scripts executed by using the `-sC` option.                                                                                     |
| `discovery`  | Evaluation of accessible services.                                                                                                      |
| `dos`        | These scripts are used to check services for denial of service vulnerabilities and are used less as it harms the services.              |
| `exploit`    | This category of scripts tries to exploit known vulnerabilities for the scanned port.                                                   |
| `external`   | Scripts that use external services for further processing.                                                                              |
| `fuzzer`     | This uses scripts to identify vulnerabilities and unexpected packet handling by sending different fields, which can take much time.     |
| `intrusive`  | Intrusive scripts that could negatively affect the target system.                                                                       |
| `malware`    | Checks if some malware infects the target system.                                                                                       |
| `safe`       | Defensive scripts that do not perform intrusive and destructive access.                                                                 |
| `version`    | Extension for service detection.                                                                                                        |
| `vuln`       | Identification of specific vulnerabilities.                                                                                             |
#### Default Scripts

```shell-session
sudo nmap <target> -sC
```

#### Specific Scripts Category

```shell-session
sudo nmap <target> --script <category>
```

#### Defined Scripts

```shell-session
sudo nmap <target> --script <script-name>,<script-name>,...
```

More information about NSE scripts and the corresponding categories we can find at: [https://nmap.org/nsedoc/index.html](https://nmap.org/nsedoc/index.html)

#### Update Scripts 

```shell-session
sudo nmap --script-updatedb
```

#### Search for Scripts 

```shell-session
find / -type f -name ftp* 2>/dev/null | grep scripts
```


#### Enable Script Tracing 

```
--script-trace
```
