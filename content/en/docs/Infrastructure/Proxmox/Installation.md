---
categories: ["Proxmox"]
tags: ["VE"]
title: "Proxmox Installation"
weight: 20
linkTitle: "Proxmox Installation"
date: 2023-01-31
description: >
  A Step-by Step guide for Proxmox Installation
---
{{% pageinfo %}}
Storage are using ZFS (RAID0)
{{% /pageinfo %}}


## Installation {#install}

I recommend you use USB Flash Drive as **Installation Medium** because it is the faster option.


### Download the installer ISO image {#download-the-installer-iso-image}

You can download ISO image from: <https://www.proxmox.com/en/downloads/category/iso-images-pve>
Currently, the latest version is **7.3-1**.


### Prepare a USB Flash Drive as Installation Medium {#prepare-a-usb-flash-drive-as-installation-medium}

Official link: <https://pve.proxmox.com/wiki/Prepare%5FInstallation%5FMedia>


#### Linux {#linux}

<!--list-separator-->

-  Find the Correct USB Device Name     :fdisk:lsblk:

    There are two ways to find out the name of the USB flash drive. The first one is use **lsblk** (strong recommend). The second way is to compare the output of the **fdisk -l** command. Both example at the below.

    ```console
    boyang:~$ lsblk
    NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda           8:0    1   3.8G  0 disk
    ├─sda1        8:1    1   242K  0 part
    ├─sda2        8:2    1   2.8M  0 part
    ├─sda3        8:3    1 859.2M  0 part /media/yanboyang713/PVE1
    └─sda4        8:4    1   300K  0 part
    nvme0n1     259:0    0 465.8G  0 disk
    ├─nvme0n1p1 259:1    0   512M  0 part /boot/efi
    └─nvme0n1p2 259:2    0 465.3G  0 part /
    ```

    OR

    ```console
    boyang:~$ sudo fdisk -l
    [sudo] password for yanboyang713:
    Disk /dev/nvme0n1: 465.8 GiB, 500107862016 bytes, 976773168 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: gpt
    Disk identifier: C60CB535-938E-4A9F-9BAC-92FDE1DD99B0

    Device           Start       End   Sectors   Size Type
    /dev/nvme0n1p1    2048   1050623   1048576   512M EFI System
    /dev/nvme0n1p2 1050624 976771071 975720448 465.3G Linux filesystem

    Disk /dev/sda: 3.8 GiB, 4081057792 bytes, 7970816 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: gpt
    Disk identifier: 50FC8F62-2C89-43B6-8D1F-C8D3CC3F8B72

    Device       Start     End Sectors   Size Type
    /dev/sda1       64     547     484   242K Microsoft basic data
    /dev/sda2      548    6307    5760   2.8M EFI System
    /dev/sda3     6308 1765843 1759536 859.2M Apple HFS/HFS+
    /dev/sda4  1765844 1766443     600   300K Microsoft basic data
    ```

<!--list-separator-->

-  Make a bootable USB using DD     :dd:bootable:usb:

    On Unix-like operating system use the dd command to copy the ISO image to the USB flash drive. First find the correct device name of the USB flash drive (see above). Then run the dd command.

    ```console
    [yanboyang713@manjaro] ➜ ~ sudo dd bs=1M conv=fdatasync if=/home/yanboyang713/Downloads/proxmox-ve.iso of=/dev/sda
    812+1 records in
    812+1 records out
    852299776 bytes (852 MB, 813 MiB) copied, 185.781 s, 4.6 MB/s
    ```


### Start Installion {#start-installion}

Office Website: <https://pve.proxmox.com/wiki/Installation>


#### Step 1: {#step-1}

When you boot from USB, You will see the below image.
![](https://pve.proxmox.com/pve-docs/images/screenshot/pve-grub-menu.png)

-   Install Proxmox VE
    Starts the normal installation.
    
    **NOTE:** It’s possible to use the installation wizard with a keyboard only. Buttons can be clicked by pressing the ALT key combined with the underlined character from the respective button. For example, ALT + N to press a Next button.

-   Install Proxmox VE (Debug mode)
    Starts the installation in debug mode. A console will be opened at several installation steps. This helps to debug the situation if something goes wrong. To exit a debug console, press CTRL-D. This option can be used to boot a live system with all basic tools available. You can use it, for example, to repair a degraded ZFS rpool or fix the bootloader for an existing Proxmox VE setup.

-   Rescue Boot
    With this option you can boot an existing installation. It searches all attached hard disks. If it finds an existing installation, it boots directly into that disk using the Linux kernel from the ISO. This can be useful if there are problems with the boot block (grub) or the BIOS is unable to read the boot block from the disk.

-   Test Memory
    Runs memtest86+. This is useful to check if the memory is functional and free of errors.

After selecting Install Proxmox VE and accepting the EULA, the prompt to select the target hard disk(s) will appear. The Options button opens the dialog to select the target file system.

The default file system is ext4. However, this testbed is using ZFS (RAID0).

**NOTE:** On file based storages, snapshots are possible with the qcow2 format.

#### Step 2: {#step-2}

![](https://pve.proxmox.com/pve-docs/images/screenshot/pve-select-location.png)
The next page asks for basic configuration options like the location, the time zone, and keyboard layout. The location is used to select a download server close by to speed up updates. The installer usually auto-detects these settings. They only need to be changed in the rare case that auto detection fails or a different keyboard layout should be used.


#### Step 3: {#step-3}

![](https://pve.proxmox.com/pve-docs/images/screenshot/pve-set-password.png)
Next the password of the superuser (root) and an email address needs to be specified. The password must consist of at least 5 characters. It’s highly recommended to use a stronger password. Some guidelines are:

-   Use a minimum password length of 12 to 14 characters.

-   Include lowercase and uppercase alphabetic characters, numbers, and symbols.

-   Avoid character repetition, keyboard patterns, common dictionary words, letter or number sequences, usernames, relative or pet names, romantic links (current or past), and biographical information (for example ID numbers, ancestors' names or dates).

The email address is used to send notifications to the system administrator. For example:

-   Information about available package updates.

-   Error messages from periodic CRON jobs.


#### Step 4: {#step-4}

![](https://pve.proxmox.com/pve-docs/images/screenshot/pve-setup-network.png)
The last step is the network configuration. Please note that during installation you can either use an IPv4 or IPv6 address, but not both. To configure a dual stack node, add additional IP addresses after the installation.


#### Step 5: {#step-5}

![](https://pve.proxmox.com/pve-docs/images/screenshot/pve-install-summary.png)
The next step shows a summary of the previously selected options. Re-check every setting and use the Previous button if a setting needs to be changed. To accept, press Install. The installation starts to format disks and copies packages to the target. Please wait until this step has finished; then remove the installation medium and restart your system.

{{< figure src="https://pve.proxmox.com/pve-docs/images/screenshot/pve-installation.png" >}}

If the installation failed check out specific errors on the second TTY (‘CTRL + ALT + F2’), ensure that the systems meets the minimum requirements. If the installation is still not working look at the how to get help chapter.

Further configuration is done via the Proxmox web interface. Point your browser to the IP address given during installation (<https://youripaddress:8006>).

## Reference List {#reference-list}

1.  <https://www.salvagedata.com/btrfs-zfs-xfs-ext4-how-are-they-different/>
2.  <https://linuxhint.com/zfs%5Fvs%5Fxfs/>
3.  <https://pve.proxmox.com/wiki/Renaming%5Fa%5FPVE%5Fnode>

