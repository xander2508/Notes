---
tags:
  - OperatingSystems
  - Linux
  - Tooling
  - Default
  - StandardInformation
---
Each logical partition or drive needs to be assigned to a specific directory on Linux. This process is called mounting. Mounting involves attaching a drive to a specific directory, making it accessible to the file system hierarchy. Once a drive is mounted, it can be accessed and manipulated just like any other directory on the system. The `mount` tool is used to mount file systems on Linux, and the `/etc/fstab` file is used to define the default file systems that are mounted at boot time.
# Guide

1. Mount all found devices (USBs etc)

# Commands 

List mounted drives:

```
mount
```

Mount USB drive:

```shell-session
sudo mount /dev/sdb1 /mnt/usb
cd /mnt/usb && ls -l
```

Unmount drive:

```shell-session
sudo umount /mnt/usb

lsof | grep user (Check if anyone is using the drive)
```