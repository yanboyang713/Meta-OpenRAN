
---
title: "GPU"
linkTitle: "GPU"
weight: 60
date: 2023-02-02
description: >
---

{{% pageinfo %}}
https://pve.proxmox.com/wiki/NVIDIA_vGPU_on_Proxmox_VE_7.x
{{% /pageinfo %}}

## Identifying the Graphics Card Model and Device ID
update your PCI ID database with:
```
sudo update-pciids
```

```console
root@server2:~# lspci -nn | grep '\[03'
0000:5b:00.0 VGA compatible controller [0300]: NVIDIA Corporation GA102 [GeForce RTX 3090] [10de:2204] (rev a1)
```


## Reference List
1. https://pve.proxmox.com/wiki/NVIDIA_vGPU_on_Proxmox_VE_7.x
2. https://cloud.google.com/compute/docs/gpus/grid-drivers-table
3. https://www.nvidia.com/Download/index.aspx
4. https://gitlab.com/polloloco/vgpu-proxmox
5. https://www.michaelstinkerings.org/using-vgpu-unlock-with-proxmox-7/
6. https://pve.proxmox.com/wiki/Pci_passthrough
