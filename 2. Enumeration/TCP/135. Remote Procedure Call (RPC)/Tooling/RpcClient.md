---
tags:
  - Enumeration
  - TCP
  - RemoteProcedureCall
  - Tooling
  - RPC
---
A complete list of all functions can be found on the [man page](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html) of the RpcClient.

[rpcclient enumeration | HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-smb/rpcclient-enumeration)
## Commands 

|**Query**|**Description**|
|---|---|
|`srvinfo`|Server information.|
|`enumdomains`|Enumerate all domains that are deployed in the network.|
|`querydominfo`|Provides domain, server, and user information of deployed domains.|
|`netshareenumall`|Enumerates all available shares.|
|`netsharegetinfo <share>`|Provides information about a specific share.|
|`enumdomusers`|Enumerates all domain users.|
|`queryuser <RID>`|Provides information about a specific user.|
## Example

```bash
rpcclient -U "" -N 10.10.10.11
```

```bash
rpcclient -p 135 -U "" 10.10.10.11
```


## Enumeration

#### Service 

```shell-session
srvinfo
```

```shell-session
enumdomains
```

```shell-session
querydominfo
```

```shell-session
netshareenumall
```

```shell-session
netsharegetinfo <SHARE>
```

#### Users

```shell-session
enumdomusers
```

Where `0x3e9` is the user ID:

```shell-session
queryuser 0x3e9
```

```shell-session
queryuser 0x3e8
```

#### Groups 

```shell-session
querygroup 0x201
```

#### Brute Forcing User RIDs

See [[Relative Identifiers (RID) and Security Identifiers (SID)]]

```shell-session
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```

An alternative to this would be a Python script from [[Impacket#SamRDump]]


## Command Cheat Sheet

![[SMB-Access-from-Linux.pdf]]