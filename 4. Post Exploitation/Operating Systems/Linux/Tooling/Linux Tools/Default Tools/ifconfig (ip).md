

# Activate Network Interface

```shell-session
sudo ifconfig eth0 up     # OR
sudo ip link set eth0 up
```

#### Assign IP Address to an Interface

```shell-session
sudo ifconfig eth0 192.168.1.2
```

#### Assign a Netmask to an Interface

```shell-session
sudo ifconfig eth0 netmask 255.255.255.0
```

#### Assign the Route to an Interface

```shell-session
sudo route add default gw 192.168.1.1 eth0
```

#### Editing DNS Settings

```shell-session
[!bash!]$ sudo vim /etc/resolv.conf
```

```txt
nameserver 8.8.8.8
nameserver 8.8.4.4
```
#### Restart Networking Service

sudo systemctl restart networking
```

# Maintain Changes

To make any changes persist across reboots edit the `/etc/network/interfaces` file, which defines network interfaces for Linux-based operating systems

```shell-session
sudo vim /etc/network/interfaces
```

```txt
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```