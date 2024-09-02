---
tags:
  - Enumeration
  - TCP
  - NetworkFileSystem
  - NFS
  - Tooling
---

[mount(8) - Linux manual page](https://www.man7.org/linux/man-pages/man8/mount.8.html)


```bash
sudo mount -t nfs 10.10.10.34:/var/nfsshare /mnt/nfsshare
```
```bash
sudo mount -t nfs -o vers=3 10.10.10.34:/var/nfsshare /mnt/nfsshare -nolock
```
