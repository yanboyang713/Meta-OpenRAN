
---
title: "Cluster"
linkTitle: "Cluster"
weight: 56
date: 2023-02-05
description: >
---

{{% pageinfo %}}
https://www.wundertech.net/how-to-set-up-a-cluster-in-proxmox/
{{% /pageinfo %}}

## Create a Cluster
Login via ssh to the first Proxmox VE node(DELL GPU Server) and run the following command:

```
pvecm create NICE-LAB(CLUSTERNAME)
```
To check the state of the new cluster use:
```
pvecm status
```
 
## Join Node to Cluster
Log in to the node you want to join into an existing cluster via ssh.
```
pvecm add IP-ADDRESS-CLUSTER
```
For IP-ADDRESS-CLUSTER, use the IP or hostname of an existing cluster node. An IP address is recommended (see Link Address Types).

To check the state of the cluster use:
```
pvecm status
```

## Reference List
1. https://www.wundertech.net/how-to-set-up-a-cluster-in-proxmox/
2. https://pve.proxmox.com/wiki/Cluster_Manager
