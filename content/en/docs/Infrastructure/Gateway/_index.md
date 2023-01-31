
---
title: "Gateway"
linkTitle: "Gateway"
weight: 1
date: 2023-01-30
description: >
  Step by step set-up Gateway
---

{{% pageinfo %}}
  Step by step set-up Gateway
{{% /pageinfo %}}

## Overview
![](https://res.cloudinary.com/dkvj6mo4c/image/upload/v1675145155/NICE-LAB/NICE-LAB_Gateway_djewfj.png)

## Installation Winbox
### Arch Linux
```console
paru -S winbox
```

## Using Winbox Login
Neighbors -> Refresh -> Click MAC address -> click Connect
**NOTE:** First time login, please use MAC address, defalt password is NULL.

## Mikrotik RouterOS Reset
### Reset from RouterOS
If you still have access to your router and want to recover its default configuration, then you can:
+ run the command "/system reset-configuration" from command line interface
+ do it from System -> Reset Configuration menu in the graphical user interface.

[Official Link](https://wiki.mikrotik.com/wiki/Manual:Reset)

## Quick Set
Mode using CPE: Client device, which will connect to an Access Point (AP) device. Provides option to scan for AP devices in your area.

### Wireless
+ Band: 2Ghz-B/G/N
+ Channel Width: 20/40Mhz XX
+ Country: united states
+ Choice WIFI as WAN, Click Signal Strength could Sort 

Click **Connect**

### Configure
+ Mode: Router

### Wireless Network
+ Address Acquisition: Automatic
+ Upload: unlimited
+ Download: unlimited

### Local Network
+ IP Address: 192.168.88.1
+ Netmask: 255.255.255.0 (/24)
+ DHCP - **Tick**
  + DHCP Server Range: 192.168.88.10 - 192.168.88.254
+ NAT - **Tick**

### System
+ Router Identity: NICE-LAB
+ Password: NICElab2023

[Official Link](https://wiki.mikrotik.com/wiki/Manual:Quickset#:~:text=Quickset%20is%20a%20simple%20configuration,of%20default%20configuration%20from%20factory.)

Final Click **Apply**, then **OK**

You could open a new Terminal, and ping google.com for testing.




