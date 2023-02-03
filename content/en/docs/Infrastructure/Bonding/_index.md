
---
title: "Console"
linkTitle: "Console"
weight: 42
date: 2023-02-02
description: >
  Console Preparation: required a Console Machine for configuration Networking and Cluster.
---

{{% pageinfo %}}
  Console Machine Preparation: we need a **Console Machine** to do some Networking and Cluster configuration.
{{% /pageinfo %}}

## Introduction
Management Console/Machine is another word for Console Machine, which will used for doing some of Networking configuration and Cluster configuration. So, we need set-up a Management Console first.

I highly recommend install [Meta Scientific Linux](https://www.metascientificlinux.com/) as your management console.
[Boyang Yan](https://www.yanboyang.com) is the main founder for this Linux Distros. If you facing any issues, please email [Boyang](mailto:yanboyang713@gmail.com).

## Create/Delete User
### Create new SUDO user
Each Testbed user should have their own sudo user. Run the following command to create a new user, for example **ostechnix**:
```console
useradd --create-home ostechnix
```

Set password to the new user:
```console
passwd ostechnix
```

We have created a new user named **ostechnix**. We haven't granted the sudo privilege to the user yet. You can verify if the user is sudo user or not using command:
```console
sudo -lU ostechnix
```
Sample output:
```
User ostechnix is not allowed to run sudo on archlinux.
```

Yes, the user is not yet allowed to perform administrative tasks. Let us go ahead and grant him the sudo permissions.

To add a normal user to sudoers list in Arch Linux, simply add him/her to the wheel group. For those wondering, the wheel is a special group in some Unix-like operating systems. All the members of wheel group are allowed to perform administrative tasks. Wheel group is similar to sudo group in Debian-based systems.

We can add users using chmod command.
To add an user to sudoers ist in Arch Linux, run:
```console
usermod -aG wheel ostechnix
```
Or,
```console
usermod --append --groups wheel ostechnix
```
The above command will add the user called ostechnix to "wheel" group. As stated already, the members of wheel group can perform administrative tasks using sudo command.
Next, edit /etc/sudoers file using command:
```
sudo vim /etc/sudoers
```
Find and uncomment the following line (just remove the # symbol at the beginning of the line):
```
%wheel ALL=(ALL) ALL
```
Hit ESC key and type :wq to save the file and exit.

Check if an user has sudo access in Arch Linux. To check if an user has sudo permissions, run:
```
sudo -lU ostechnix
```
Sample output:
```
User ostechnix may run the following commands on archlinux:
    (ALL) ALL
```

### Delete sudo privileges from an user in Arch Linux
We can take away the sudo privileges from an user without actually having to delete the user.

First, log out from the user and log back in as root or another sudo user. Next, delete sudo privileges from an user by simply removing him/her from the wheel group using the following command in Arch Linux:
```
gpasswd -d ostechnix wheel
```
If you have added the user to sudo group, you need to remove him/her from that group too.
```
gpasswd -d ostechnix sudo
```
That's it. The user is not in the sudoers list anymore, so he can't run any administrative tasks.

You can verify it using command:
```
sudo -lU ostechnix
```

If you don't want that user anymore, remove him entirely from the system using this command:

```
userdel -r ostechnix
```

Here, -r flag is used to delete the **$HOME** directory of the user.

## User logout
Each user when finished to use management console, please logout for your account.

### I3 WM
1. Win + 0
2. e(xit)

### Meta WM
Run command:
```
sudo pkill -KILL -u YourUserName
```

## Reference List
1. https://ostechnix.com/add-delete-and-grant-sudo-privileges-to-users-in-arch-linux/
