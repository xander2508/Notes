---
tags:
  - Enumeration
  - TCP
  - RemoteProcedureCall
  - Tooling
---
A complete list of all functions can be found on the [man page](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html) of the RpcClient.


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