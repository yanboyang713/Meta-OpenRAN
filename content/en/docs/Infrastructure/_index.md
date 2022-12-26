
---
title: "Infrastructure"
linkTitle: "Infrastructure"
weight: 2
date: 2017-01-05
description: >
  List all of required infrastucture
---

{{% pageinfo %}}
List all of required infrastucture
{{% /pageinfo %}}

Part 1:
Overview:
https://res.cloudinary.com/dkvj6mo4c/image/upload/v1666064185/Open-RAN/Edge-Cloud_gxiuck.png

+ mikrotik RouterOS license backup
https://techoverflow.net/2022/08/23/how-to-backup-mikrotik-routeros-license-to-a-file/

+ Mikrotik RouterOS connect Uni WIFI: eduroam
When you done, login Yuchen account

+ Mikrotik RouterOS Gateway set-up
Please check: https://www.yanboyang.com/chronproxmox/#step-4-start-your-ros

+ Proxmox VE Install
https://www.proxmox.com/en/downloads/category/iso-images-pve

https://www.yanboyang.com/proxmoxinstall/

+ Proxmox VE VXLAN set-up
https://pve.proxmox.com/pve-docs/chapter-pvesdn.html

Please, check with OVS: http://www.openvswitch.org/
TWO ports for Computing, and two ports for Storage.

https://pve.proxmox.com/wiki/Open_vSwitch
Please, check Example 2: Bond + Bridge + Internal Ports

We also need Ceph cluster

+ Ceph cluster Set-up
We have 3-node, if need buy HHD/SSD, please lets us know.
Reference:
1. https://packetpushers.net/proxmox-ceph-full-mesh-hci-cluster-w-dynamic-routing/
2. https://pve.proxmox.com/wiki/Deploy_Hyper-Converged_Ceph_Cluster
pveceph CLI tool could useful

+ Blobfuse2 set-up
https://github.com/Azure/azure-storage-fuse

You can based on File Cashe Config
https://github.com/Azure/azure-storage-fuse/blob/main/sampleFileCacheConfig.yaml

I will give you my Azure Data lake(ADLS) access key, you need NOT create ADLS by yourself.
Mount DIR to our Ceph cluster.

+ K3S or K8S create
If you never use K8S, please check: https://www.yanboyang.com/k8s/

K3s is a Kubernetes distribution that aims to simplify Kubernetes deployments. Kubernetes is an open-source container orchestration system for automating software deployment, scaling, and management.
https://k3s.io/img/how-it-works-k3s-revised.svg

If you want to create K8S, it will be good.
You could look Ansible and Terraform

K3S also fine, if you don't want to set-up K8S
you could use: autok3s
https://github.com/cnrancher/autok3s/blob/master/docs/i18n/en_us/native/README.md

This is all for Part One. When you done Part One, Please lets me know.

Part Two:
All of below services, please deploy to K8S or K3S

+ set-up package manager for Kubernetes
You also could look at others PM
Helm V2
Helm helps you manage Kubernetes applications — Helm Charts help you define, install, and upgrade even the most complex Kubernetes application.
Charts are easy to create, version, share, and publish — so start using Helm and stop the copy-and-paste.

+ Install POSTGRESQL
https://bitnami.com/stack/postgresql/helm

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


