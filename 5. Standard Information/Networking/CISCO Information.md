---
tags:
  - Networking
---
Cisco switches provide the `VLAN` IDs/numbers 1-4094 (`0` and `4095` are reserved IDs and cannot be used); IDs 1-1005 (`VLAN 1` is known as the `default VLAN` and cannot/should not be altered nor deleted) are known as `normal-range` `VLANs`, with IDs 1002-1005 being reserved for `Token Ring` and `Fiber Distributed Data Interface` (`FDDI`) `VLANs`, while IDs 1006-4094 are known as `extended-range` `VLANs`. By default, any customization applied for `normal-range` `VLANs` is saved in the `VLAN` database (the `vland.dat` file), in contrast to `extended-range` `VLANs`, which do not have their customizations saved. `VLANs` 2-1001 stored in `vlan.dat` can have parameters including name, type, state, and maximum transmission unit (`MTU`).