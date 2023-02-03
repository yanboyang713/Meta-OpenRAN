
---
title: "Infrastructure"
linkTitle: "Infrastructure"
weight: 40
date: 2023-01-31
description: >
  All of required infrastucture set up
---

{{% pageinfo %}}
All of required infrastucture set up guideline and INFO.
{{% /pageinfo %}}

## Console - DONE
[More details, please check](./console/)

## Gateway - DOME
Our Testbed Gateway **LAN** INFO:
  + MAC Address: **DC:2C:6E:3E:01:45**
  + Ip Address: **192.168.88.1**
  + User Name: admin
  + Password: NICElab2023

NICE Lab Gateway **WAN** INFO:
  + IP Address: 10.154.6.207
  + Netmask: 255.255.192.0 (/18)
  + Gateway: 10.154.0.1

[More details, please check](./gateway/)

## Proxmox VE - DONE
  - Server 1:
    - Hostname: server1.nicelab.us
    - E-mail: byan4@ncsu.edu
    - Password:  NICElab2023
    - IP Address: 192.168.88.4/24
    - Gateway: 192.168.88.1
    - DNS Server: 192.168.88.1
    - Web GUI: https://192.168.88.4:8006
    - Note: CPU server
  
  - Server 2:
    - Hostname: server2.nicelab.us
    - E-mail: byan4@ncsu.edu
    - Password: NICElab2023
    - IP Address: 192.168.88.3/24
    - Gateway: 192.168.88.1
    - DNS Server: 192.168.88.1
    - Web GUI: https://192.168.88.3:8006
    - Note: GPU server
    
  - Server 3:
    - Hostname: server3.nicelab.us
    - E-mail: byan4@ncsu.edu
    - Password: NICElab2023
    - IP Address: 192.168.88.2/24
    - Gateway: 192.168.88.1
    - DNS Server: 192.168.88.1
    - Web GUI: https://192.168.88.2:8006
    - Note: CPU server

[More details, please check](./proxmox/)



# Part 1:
Overview:
https://res.cloudinary.com/dkvj6mo4c/image/upload/v1666064185/Open-RAN/Edge-Cloud_gxiuck.png



+ mikrotik RouterOS license backup
https://techoverflow.net/2022/08/23/how-to-backup-mikrotik-routeros-license-to-a-file/

+ mikrotik RouterOS System backup
https://wiki.mikrotik.com/wiki/Manual:System/Backup

+ Mikrotik RouterOS connect Uni WIFI: eduroam
When you done, login Yuchen account

+ Mikrotik RouterOS Gateway set-up
Please check: https://www.yanboyang.com/chronproxmox/#step-4-start-your-ros


+ Proxmox VE VXLAN set-up
https://pve.proxmox.com/pve-docs/chapter-pvesdn.html

Please, check with OVS: http://www.openvswitch.org/
TWO ports for Computing, and two ports for Storage.

https://pve.proxmox.com/wiki/Open_vSwitch
Please, check Example 2: Bond + Bridge + Internal Ports

+ Mikrotik RouterOS Bond set-up

+ Set-up Blobfuse2
https://github.com/Azure/azure-storage-fuse

Sample Configuration File in the attachment, named fileCacheConfig-test.yaml with access key

You may follow the steps like mount blobfuse2 with Docker
https://github.com/Azure/azure-storage-fuse/tree/main/docker

You can based on File Cashe Config
https://github.com/Azure/azure-storage-fuse/blob/main/sampleFileCacheConfig.yaml

My Azure Data lake(ADLS) access key already give to you, you need NOT create ADLS by yourself.

Mount DIR to RAM for now.

+ K3S or K8S create
If you never use K8S, please check
https://www.yanboyang.com/k8s/

K3s is a Kubernetes distribution that aims to simplify Kubernetes deployments. Kubernetes is an open-source container orchestration system for automating software deployment, scaling, and management.
https://k3s.io/img/how-it-works-k3s-revised.svg

If you want to create K8S, it will be good.
You could look Ansible and Terraform

K3S also fine, if you don't want to set-up K8S
you could use: autok3s
https://github.com/cnrancher/autok3s/blob/master/docs/i18n/en_us/native/README.md

+ Mount Blobfuse2 with K3S/K8S. You may check CSI
https://kubernetes.io/blog/2019/01/15/container-storage-interface-ga/

+ set-up package manager for Kubernetes
You also could look at others PM
Helm V2
Helm helps you manage Kubernetes applications — Helm Charts help you define, install, and upgrade even the most complex Kubernetes application.
Charts are easy to create, version, share, and publish — so start using Helm and stop the copy-and-paste.

+ Install POSTGRESQL
https://bitnami.com/stack/postgresql/helm

This is all for Part One. When you done Part One, Please lets me know.

# Part Two:
We also need Ceph cluster

+ Ceph cluster Set-up
We have 3-node, if need buy HHD/SSD, please lets us know.
Reference:
1. https://packetpushers.net/proxmox-ceph-full-mesh-hci-cluster-w-dynamic-routing/
2. https://pve.proxmox.com/wiki/Deploy_Hyper-Converged_Ceph_Cluster
pveceph CLI tool could useful

All of below services, please deploy to K8S or K3S

+ Istio service mesh set-up
A service mesh is a dedicated infrastructure layer for facilitating service-to-service communications between services or microservices, using a proxy.

+ Set-up Hudi (Data lake)
https://hudi.apache.org/
Hudi is a rich platform to build streaming data lakes with incremental data pipelines on a self-managing database layer, while being optimized for lake engines and regular batch processing.
https://hudi.apache.org/assets/images/hudi-lake-5a04ad2714a694321af4d0cb570dc486.png

+ Set-up Flink
We need Flink as ML/DL training Cluster.

Please, deploy Flink first.

Apache Flink is an open-source, unified stream-processing and batch-processing framework. Flink executes arbitrary dataflow programs in a data-parallel and pipelined.

When you done Flink set-up, please check below link: DL on Flink with Tensorflow and PyTorch.

Make sure at least one example could woprks for each.

Deep Learning on Flink: https://github.com/flink-extended/dl-on-flink

Deep Learning on Flink aims to integrate Flink and deep learning frameworks (e.g. TensorFlow, PyTorch, etc.) to enable distributed deep learning training and inference on a Flink cluster.

+ Set-up Airflow
https://airflow.apache.org/
Apache Airflow is an open-source workflow management platform for data engineering pipelines.

+ Set-up Log system
We will use C++, Rust, Python, and R.
Please, check vector and prometheus
https://vector.dev/
https://prometheus.io/

+ Rook
Rook is an open source cloud-native storage orchestrator, providing the platform, framework, and support for Ceph storage to natively integrate with cloud-native environments.
https://rook.io/docs/rook/v1.10/Getting-Started/intro/
