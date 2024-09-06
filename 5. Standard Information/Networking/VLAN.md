---
tags:
  - Networking
  - StandardInformation
---
# Creating a VLAN 
## Linux 

In Linux, creating a `VLAN` is done by creating an interface on top of another, called a `parent` interface. This `VLAN` interface will tag packets with the assigned `VLAN` ID while returning packets will be untagged.

To assign a network adapter a `VLAN` in Linux, many tools can be used, such as [ip](https://man7.org/linux/man-pages/man8/ip.8.html), [nmcli](https://linux.die.net/man/1/nmcli), and [vconfig](https://linux.die.net/man/8/vconfig) (deprecated). However, first, we need to ensure that the Kernel has the [802.1Q](https://elixir.bootlin.com/linux/v6.4.7/source/net/8021q/vlan.c) module loaded:

  VLANs

```shell-session
AlexanderOrley@htb[/htb]$ sudo modprobe 8021q
```

Subsequently, we can use `lsmod` to make sure `8021q` was loaded successfully:

  VLANs

```shell-session
AlexanderOrley@htb[/htb]$ lsmod | grep 8021

8021q                  40960  0
garp                   16384  1 8021q
mrp                    20480  1 8021q
```

Now, we need to find the name of the physical `Ethernet` interface that we will create the `VLAN` interface on top of, which is `eth0`:

  VLANs

```shell-session
AlexanderOrley@htb[/htb]$ ip a

<SNIP>
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether a6:ba:3b:08:3a:36 brd ff:ff:ff:ff:ff:ff
    altname enp0s3
    altname ens3
    inet 94.2X.5X.72/22 brd 94.237.51.255 scope global dynamic eth0
       valid_lft 83489sec preferred_lft 83489sec
    inet6 fe80::a4ba:3bff:fe08:3a36/64 scope link 
       valid_lft forever preferred_lft forever
```

Then, we will use `vconfig` to create a new interface that is a member of the desired `VLAN`, `20`, for example, on top of `eth0`:

  VLANs

```shell-session
AlexanderOrley@htb[/htb]$ sudo vconfig add eth0 20

Warning: vconfig is deprecated and might be removed in the future, please migrate to ip(route2) as soon as possible!
```

To use `ip` instead:

  VLANs

```shell-session
sudo ip link add link eth0 name eth0.20 type vlan id 20
```

Either of these commands will make a new interface called `eth0.20@eth0`:

  VLANs

```shell-session
AlexanderOrley@htb[/htb]$ ip a

<SNIP>
4: eth0.20@eth0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether a6:ba:3b:08:3a:36 brd ff:ff:ff:ff:ff:ff
```

Then, based on the `subnet` assigned to the addresses with `VLAN 20` within the local network, we need to assign the interface an IP address and then start it:

  VLANs

```shell-session
AlexanderOrley@htb[/htb]$ sudo ip addr add 192.168.1.1/24 dev eth0.20
AlexanderOrley@htb[/htb]$ sudo ip link set up eth0.20
```

At last, we can check whether the interface has changed states to up:

  VLANs

```shell-session
AlexanderOrley@htb[/htb]$ ip a | grep eth0.20

4: eth0.20@eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    inet 192.168.1.1/24 scope global eth0.20
```

## Windows 

On Windows, to assign a `VLAN` for a physical network adapter that supports `VLAN tagging`, first we need to open `Device Manager`:

![Windows_Device_Manager.png](https://academy.hackthebox.com/storage/modules/34/Windows_Device_Manager.png)

Then we need to click on `Properties` for the `Ethernet interface` we want to assign to a `VLAN`:

![Windows_Device_Manager_Adapter_Properties.png](https://academy.hackthebox.com/storage/modules/34/Windows_Device_Manager_Adapter_Properties.png)

Within `Advanced`, there will be a `VLAN ID` property to which we can assign a value. After clicking `OK`, if the adapter supports assigning a `VLAN`, it will be set; otherwise, the window will close, and no `VLAN` tag will be added to any packets originating from this host:

![Windows_Device_Manager_Adapter_Properties_VLAN_ID.png](https://academy.hackthebox.com/storage/modules/34/Windows_Device_Manager_Adapter_Properties_VLAN_ID.png)

Instead of relying on the GUI, we can use `PowerShell`. First, let us get the names of all the available physical network adapters using the [Get-NetAdapter](https://learn.microsoft.com/en-us/powershell/module/netadapter/get-netadapter?view=windowsserver2022-ps) Cmdlet:


```powershell-session
PS C:\> Get-NetAdapter | Format-Table -AutoSize

Name                                           InterfaceDescription                                                          ifIndex Status             MacAddress              LinkSpeed
----                                           --------------------                                                          ------- ------             ----------              ---------
VirtualBox Host-Only Network  VirtualBox Host-Only Ethernet Adapter                                        20 Up                    0A-00-27-10-42-15       1 Gbps
Ethernet 2                                 ASIX AX88772B USB2.0 to Fast Ethernet Adapter                            55 Up                    90-EB-78-14-21-7F    100 Mbps
Bluetooth Network Connection  Bluetooth Device (Personal Area Network)                                   18 Disconnected   38-41-25-E8-DE-2D        3 Mbps
Wi-Fi                                         Intel(R) Wireless-AC 9560 160MHz                                                12 Disconnected   8E-36-6A-7A-BA-6A 866.7 Mbps
```

Previously, we used `Device Manager` to assign `Ethernet 2` to `VLAN 10`; to retrieve the `VLAN` ID of the interface, we can use the [Get-NetAdapaterAdvancedProperty](https://learn.microsoft.com/en-us/powershell/module/netadapter/get-netadapteradvancedproperty?view=windowsserver2022-ps) Cmdlet with the `-DisplayName` flag along with `vlan id`:

```powershell-session
PS C:\> Get-NetAdapterAdvancedProperty -DisplayName "vlan id"

Name                      DisplayName                    DisplayValue                   RegistryKeyword RegistryValue
----                      -----------                    ------------                   --------------- -------------
Ethernet 2                VLAN ID                        10                                     VLAN_ID               {10}
```

We can also set the `VLAN` ID of a physical network address using the [Set-NetAdapter](https://learn.microsoft.com/en-us/powershell/module/netadapter/set-netadapter?view=windowsserver2022-ps) Cmdlet along with the [VlanID](https://learn.microsoft.com/en-us/powershell/module/netadapter/set-netadapter?view=windowsserver2022-ps#-vlanid) flag; this powerful Cmdlet can also be used to customize other properties of interfaces such as [MAC addresses](https://learn.microsoft.com/en-us/powershell/module/netadapter/set-netadapter?view=windowsserver2022-ps#-macaddress):

```powershell-session
PS C:\> Set-NetAdapter -Name "Ethernet 2" -VlanID 10
```

However, remember that this operation only succeeds if the network interface supports this functionality; otherwise, `PowerShell` will throw an error indicating that the interface does not support it.

# Vulnerabilities  

#### VLAN Hopping

`VLAN hopping` attacks enable traffic from one `VLAN` to be seen by another `VLAN` without the aid of a router. It exploits Cisco's `Dynamic Trunking Protocol` (`DTP`), a protocol used to automatically negotiate the formation of a `trunk link` between two Cisco devices. An adversary needs to configure a host to mimic/act like a switch to take advantage of the automatic trunking port feature enabled by default on most switch ports. To exploit `VLAN hopping`, an adversary must be able to physically connect with a switch port that has `DTP` enabled. The adversary can abuse this connection by configuring a host connected to the switch on that specific port to spoof `802.1Q` signalling and the `DTP` packets. If successful, the switch will eventually establish a `trunk link` with the adversary's host, exposing the network packets, not only for a specific `VLAN`.

#### Double-tagging VLAN Hopping

The `double-tagging VLAN hopping attack` is an increasingly more sophisticated attack against `VLANs`. Although `VLAN double-tagging` is a legitimate practice that entities such as `Internet Service Providers` (`ISPs`) utilize (they can use their `VLANs` internally while carrying traffic from clients that are already `VLAN tagged`), adversaries can also attempt to abuse it. In a `double-tagging VLAN hopping attack`, an adversary embeds a hidden `802.1Q` tag inside an `Ethernet` frame that already has an `802.1Q` tag, allowing the frame to go to a different `VLAN`, which the original `802.1Q` tag did not specify.

# VXLAN

We mentioned previously that the `VID` field within the '802.1Q' header inside an 'Ethernet' frame is only 12 bits, allowing for 4094 VLANs. While this number of VLANs might be sufficient for small networks, more is needed for data centers and cloud service providers, which require extensive segmentation. Additionally, current Layer 2 networks utilize the `IEEE 802.1D` `Spanning Tree Protocol` (`STP`) to prevent network loops caused by redundant paths. However, some data center operators encounter limitations with `STP`, such as link blocking, which reduces available ports and prevents resiliency through multipathing. These challenges hinder network efficiency in virtualized environments that rely on Layer 2 physical infrastructure. A critical requirement in such environments is the seamless scalability of the Layer 2 network across the entire data center and even between data centers to allocate computing, networking, and storage resources efficiently. Nevertheless, traditional approaches like `STP`, while ensuring a loop-free topology, can deactivate many links, further exacerbating the problem.

[RFC7348](https://datatracker.ietf.org/doc/html/rfc7348) offers a solution to these problems and limitations in Layer 2 networks by introducing `Virtual eXtensible Local Area Network` (`VXLAN`), which is essentially a 'Layer 2 overlay scheme on a Layer 3 network.' `VXLAN` is specifically designed to address the limitations of traditional Layer 2 networks and cater to the requirements of Layer 2 and Layer 3 data center network infrastructures in a multi-tenant environment with virtual machines (VMs). Operating over the existing networking infrastructure, `VXLAN` provides an innovative way to seamlessly extend a Layer 2 network. Its primary objective is to facilitate the scaling of Layer 2 networks across expansive data center landscapes, even spanning multiple physical data locations. Each `VXLAN` overlay is termed a `VXLAN segment`, ensuring that only VMs within the same VXLAN segment can communicate with each other, thus maintaining network isolation and security. A 24-bit segment ID, known as the `VXLAN Network Identifier` (`VNI`), uniquely identifies each VXLAN segment. Adopting VXLAN allows for the coexistence of 16 million `VXLAN` segments within the same administrative domain, providing scalability and flexibility for modern data centers and virtualized environments.

