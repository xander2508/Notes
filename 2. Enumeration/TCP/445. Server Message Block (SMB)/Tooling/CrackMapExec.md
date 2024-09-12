---
tags:
  - Enumeration
  - TCP
  - ServerMessageBlock
  - SMB
  - Tooling
---


[GitHub - byt3bl33d3r/CrackMapExec: A swiss army knife for pentesting networks](https://github.com/byt3bl33d3r/CrackMapExec)


```shell-session
crackmapexec smb 10.129.14.128 --shares -u '' -p ''
```

## Installation

```shell-session
sudo apt-get -y install crackmapexec
```

## Usage

### Options

```shell-session
usage: crackmapexec [-h] [-t THREADS] [--timeout TIMEOUT]
                    [--jitter INTERVAL] [--darrell]
                    [--verbose]
                    {mssql,smb,ssh,winrm} ...

optional arguments:
  -h, --help            show this help message and exit
  -t THREADS            set how many concurrent threads to use (default: 100)
  --timeout TIMEOUT     max timeout in seconds of each thread (default: None)
  --jitter INTERVAL     sets a random delay between each connection (default: None)
  --darrell             give Darrell a hand
  --verbose             enable verbose output

protocols:
  available protocols

  {mssql,smb,ssh,winrm}
    mssql               own stuff using MSSQL
    smb                 own stuff using SMB
    ssh                 own stuff using SSH
    winrm               own stuff using WINRM
```