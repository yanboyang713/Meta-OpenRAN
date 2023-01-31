---
categories: ["Proxmox"]
tags: ["VE", "Renaming"]
title: "Proxmox Renaming"
weight: 3
linkTitle: "Proxmox Renaming"
date: 2023-01-31
description: >
  A Step-by Step guide for Proxmox Renaming
---
## Renaming a PVE node {#renaming-a-pve-node}

/etc/hosts:

```text
127.0.0.1 localhost.localdomain localhost
10.172.14.61 pve.richie.corp.microsoft.com richie

## The following lines are desirable for IPv6 capable hosts

::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
```

/etc/hostname:

```text
richie
```
