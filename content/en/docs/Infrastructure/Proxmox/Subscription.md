---
categories: ["Proxmox"]
tags: ["VE", "Subscription"]
title: "Proxmox Subscription"
weight: 2
linkTitle: "Proxmox Subscription"
date: 2023-01-31
description: >
  A Step-by Step guide for Proxmox Installation
---
## How to update Proxmox without buying a subscription {#how-to-update-proxmox-without-buying-a-subscription}

On the Proxmox website, they say: “Proxmox VE is a complete open-source platform for enterprise virtualization.” And typically you can’t charge for open source software; but the folks at Proxmox have done their best to scare most of us into buying a subscription — or, at least, to make us feel guilty for not having one.

Now, Proxmox is great software; and developing great software takes great resources, great developers… and great money. As such, I encourage you to purchase a subscription if you’re using Proxmox in a business environment. However, some of you may be interested in using it for home usage, or just to tinker around, and for any of a variety of reasons you may not wish to, or may not be able to, purchase a subscription. This section is for you.

To be clear, Proxmox works just fine without a license. The non-licensed version is just as functional as the paid version, with one exception: it doesn’t have access to the tested “enterprise” update repositories. As such (without the changes I’m about to show you), you can’t update the Debian software. Oh and of course, there’s that little nag screen each time you log in.

SSH into the Proxmox host, or access its console through the web interface, and make a copy of the pve-enterprise.list sources file, like so:

1.  Step 1:

    ```bash
       root@pve ~# cd /etc/apt/sources.list.d/
    ```

2.  Step 2:

    ```bash
       root@pve ~# cp pve-enterprise.list pve-no-subscription.list
    ```

3.  Step 3:
    OK, so now we have a copy of the original file. If we ever purchase a subscription later and want to use the enterprise repositories, we’ll be able to revert what we’ve done very easily. For now, edit the original file and comment out its one line; save and close the file.

4.  Step 4:
    Open the copied file, pve-no-subscription.list, and change the line ever so slightly. The original line looks something like this:

    ```text
       deb https://enterprise.proxmox.com/debian/pve buster pve-enterprise
    ```

    The parts to note are https (change it to http,) enterprise.proxmox.com (change enterprise to download), and the end of the string — pve-enterprise (change to pve-no-subscription ). Do not edit the word stretch or buster, or any other word that appears in that position; that’s the Debian version code name. Your edited line should look like this:

    ```text
       deb http://download.proxmox.com/debian/pve buster pve-no-subscription
    ```

    Save and close the file. Now, update the package lists

5.  Step 5:

    ```bash
       root@pve ~# apt-get update
    ```

6.  Step 6: And when that’s done, run software upgrades!

    ```bash

       root@pve ~# apt-get dist-upgrade
    ```

    **Note:** Always run dist-upgrade, not just "apt-get upgrade." Dist-upgrade ensures that all packages and their dependencies are updated; if you just run “apt-get upgrade” things may break.
