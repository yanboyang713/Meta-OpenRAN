
---
title: "LXC Container"
linkTitle: "LXC"
weight: 62
date: 2023-02-06
description: >
---

{{% pageinfo %}}
LXC: https://www.yanboyang.com/lxccontainerproxmox/
{{% /pageinfo %}}

## Introduction
Containers are a **lightweight** alternative to fully virtualized machines (VMs). They use the kernel of the host system that they run on, instead of emulating a full operating system (OS). This means that containers can access resources on the host system directly.

The runtime costs for containers is low, usually negligible. However, there are some drawbacks that need be considered:
+ Only Linux distributions can be run in LXC Containers. It is not possible to run other operating systems like, for example, FreeBSD or Microsoft Windows inside a container.
+ For security reasons, access to host resources needs to be restricted. Therefore, containers run in their own separate namespaces. Additionally some syscalls (user space requests to the Linux kernel) are not allowed within containers.

## LXC
Proxmox VE uses Linux Containers (LXC) as its underlying container technology. The “Proxmox Container Toolkit” (pct) simplifies the usage and management of LXC, by providing an interface that abstracts complex tasks.

Containers are tightly integrated with Proxmox VE. This means that they are aware of the cluster setup, and they can use the same network and storage resources as virtual machines. You can also use the Proxmox VE firewall, or manage containers using the HA framework.

The primary goal is to offer an environment that provides the benefits of using a VM, but without the additional overhead. This means that Proxmox Containers can be categorized as “System Containers”, rather than “Application Containers”.

**NOTE:**
If you want to run application containers, for example, Docker images, it is recommended that you run them inside a Proxmox Qemu VM. This will give you all the advantages of application containerization, while also providing the benefits that VMs offer, such as strong isolation from the host and the ability to live-migrate, which otherwise isn’t possible with containers.

## Container Images Download
Container images, sometimes also referred to as “templates” or “appliances”, are tar archives which contain everything to run a container.

Proxmox VE itself provides a variety of basic templates for the most common Linux distributions. They can be downloaded using the GUI or the pveam (short for Proxmox VE Appliance Manager) command line utility. Additionally, TurnKey Linux container templates are also available to download.

The list of available templates is updated daily through the pve-daily-update timer. You can also trigger an update manually by executing:

```bash
pveam update
```

To view the list of available images run:
```bash
pveam available
```


You can restrict this large list by specifying the section you are interested in, for example basic system images:
List available system images

```console
root@richie:~# pveam available --section system
system          alpine-3.11-default_20200425_amd64.tar.xz
system          alpine-3.12-default_20200823_amd64.tar.xz
system          archlinux-base_20200508-1_amd64.tar.gz
system          archlinux-base_20201116-1_amd64.tar.gz
system          centos-7-default_20190926_amd64.tar.xz
system          centos-8-default_20191016_amd64.tar.xz
system          debian-10-standard_10.5-1_amd64.tar.gz
system          debian-9.0-standard_9.7-1_amd64.tar.gz
system          fedora-32-default_20200430_amd64.tar.xz
system          fedora-33-default_20201115_amd64.tar.xz
system          gentoo-current-default_20200310_amd64.tar.xz
system          opensuse-15.2-default_20200824_amd64.tar.xz
system          ubuntu-16.04-standard_16.04.5-1_amd64.tar.gz
system          ubuntu-18.04-standard_18.04.1-1_amd64.tar.gz
system          ubuntu-20.04-standard_20.04-1_amd64.tar.gz
system          ubuntu-20.10-standard_20.10-1_amd64.tar.gz
root@richie:~# 
```

Before you can use such a template, you need to download them into one of your storages. If you’re unsure to which one, you can simply use the local named storage for that purpose. For clustered installations, it is preferred to use a shared storage so that all nodes can access those images.

```bash
pveam download local ubuntu-22.10-standard_22.10-1_amd64.tar.zst
```

```console
root@richie:~# pveam list local
NAME                                                         SIZE  
local:vztmpl/ubuntu-20.04-standard_20.04-1_amd64.tar.gz      204.28MB
root@richie:~#
```

## Steps for create a new LXC Container
1. Open **Proxmox** web
2. Select **Server View** then select your **Node** then click on **Create CT**
![](https://www.hostfav.com/blog/wp-content/uploads/2017/08/crateCT1-768x231.jpg)
3. Enter **hostname** and **Password**
![](https://www.hostfav.com/blog/wp-content/uploads/2017/08/crateCT2.jpg)
4. Select Template Storage and then Select OS from Dropdown List and click on Next
![](https://www.hostfav.com/blog/wp-content/uploads/2017/08/crateCT3.jpg)
5. Enter **Disk Size**
6. Enter **Number of CPU Cores**
7. Enter **RAM** size in **MB**
8. Enter **Network** Details
9. Enter **Name Servers** Details
10. Click on **Finish**

Wait for the task to complete.
![](https://www.hostfav.com/blog/wp-content/uploads/2017/08/crateCT5-768x394.jpg)
You **Proxmox** Container is ready.

## Reference List
1. https://pve.proxmox.com/wiki/Linux_Container
