---
tags:
  - OperatingSystems
  - Windows
  - Services
---
[SC](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc754599(v=ws.11)) is a Windows executable utility that allows us to query, modify, and manage host services locally and over the network. Other tools, like [[Windows Management Instrumentation Command (WMIC)]] and [[Tasklist]] that can also query and manage services for local and remote hosts.

The `sc qc` command is used to query the service. This is where knowing the names of services can come in handy. If we wanted to query a service on a device over the network, we could specify the hostname or IP address immediately after `sc`.

# Query All Active Services

```cmd-session
sc query type= service
```

# Query One Service 

```cmd-session
sc query windefend    
```

# Stopping and Starting Services

Certain processes are protected under stricter access requirements than what local administrator accounts have.

```cmd-session
sc stop wuauserv
```

```cmd-session
sc start wuauserv
```

# Modifying Services

To configure services, we must use the [config](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sc-config) parameter in `sc`. All changes made with this command are reflected in the Windows registry as well as the database for Service Control Manager (`SCM`). Remember that all changes to existing services will only fully update after restarting the service.

> [!NOTE]
> It is important to be aware that modifying existing services can effectively take them out permanently as any changes made are recorded and saved in the registry, which can persist on reboot. Please exercise caution when modifying services in this manner.

## Disabling Service 

```cmd-session
sc config wuauserv start= disabled
```

To revert everything back to normal, you can set `start= auto`



```cmd-session
sc qc wuauserv
```

```cmd-session
sc //hostname or ip of box query ServiceName
```

We can also use sc to start and stop services.


Another helpful way we can examine service permissions using `sc` is through the `sdshow` command.

```cmd-session
sc sdshow wuauserv

D:(A;;CCLCSWRPLORC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;SY)S:(AU;FA;CCDCLCSWRPWPDTLOSDRCWDWO;;;WD)
```
See [[Objects and Security Descriptors]] for explanation on how to read this output. However, for a human readable output, see:

```powershell-session
Get-ACL -Path HKLM:\System\CurrentControlSet\Services\wuauserv | Format-List
```