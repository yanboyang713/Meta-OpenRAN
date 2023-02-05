
---
title: "Bonding"
linkTitle: "Bonding"
weight: 54
date: 2023-02-02
description: >
---

{{% pageinfo %}}
https://docs.openvswitch.org/en/latest/topics/bonding/
{{% /pageinfo %}}

## Install Open vSwitch {#install-open-vswitch}

Update the package index and then install the Open vSwitch and ifupdown2 packages by executing:
**NOTE:** In the version of Proxmox we are using, the package ifupdown2 is installed. Why is that important? Originally in Debian you have to reboot the whole server in order to apply changes to network settings. The ifupdown2 package allows us to apply changes without the reboot.
```console
apt update
apt install ifupdown2
apt install openvswitch-switch
```

Before edit **/etc/network/interfaces**, please backup this file.
```
cp /etc/network/interfaces /etc/network/interfaces.backup
```
Editing:
```
vi /etc/network/interfaces
```
File:
```
auto lo
iface lo inet loopback

auto enp1s0
iface enp1s0 inet manual

auto enp2s0
iface enp2s0 inet manual

auto enp3s0
iface enp3s0 inet manual

auto enp4s0
iface enp4s0 inet manual

auto enp5s0
iface enp5s0 inet manual

auto enp6s0
iface enp6s0 inet manual

auto vlan1
iface vlan1 inet static
        address 192.168.88.4/24
        gateway 192.168.88.1
        ovs_type OVSIntPort
        ovs_bridge vmbr0
        ovs_options vlan_mode=access
        ovs_extra set interface ${IFACE} external-ids:iface-id=$(hostname -s)-${IFACE}-vif
        dns-nameservers 192.168.88.1 8.8.8.8 8.8.4.4

auto bond0
iface bond0 inet manual
        ovs_bonds enp1s0 enp2s0 enp3s0 enp4s0 enp5s0
        ovs_type OVSBond
        ovs_bridge vmbr0
        ovs_options vlan_mode=native-untagged bond_mode=balance-slb

auto vmbr0
iface vmbr0 inet manual
        ovs_type OVSBridge
        ovs_ports bond0 vlan1
```
Apply:
```
ifreload -a
ifup vmbr0
```

```
/interface bridge port
remove [ find interface=ether1 ]
remove [ find interface=ether2 ]
remove [ find interface=ether3 ]
remove [ find interface=ether4 ]
remove [ find interface=ether5 ]
```
To move to the top level again, type " / "

```
/interface bonding add mode=balance-alb slaves=ether1,ether2,ether3,ether4,ether5 primary=ether1 name=bond1
```

```
/interface bridge port
add bridge=bridge interface=bond1
```

Speed Test:
```
/tool/speed-test address=192.168.88.1
```
## Reference List
1. https://docs.openvswitch.org/en/latest/topics/bonding/
2. https://karneliuk.com/2021/08/infrastructure-1-building-virtualized-environment-with-debian-linux-and-proxmox-on-hp-and-supermicro/
