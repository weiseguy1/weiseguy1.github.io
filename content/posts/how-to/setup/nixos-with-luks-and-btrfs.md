---
title: "How to Setup NixOS with LUKS and BTRFS"
date: 2024-05-30T06:02:02-05:00
description: "A BTR-y smooth installation"
draft: false
type: "post"
tags: ["nixos", "how-to", "linux"]
showTableOfContents: true
---

![Cover Image](/images/posts/how-to/setup/nixos-with-luks-and-btrfs/cover.png)

# Introduction

Recently I've been seeing a lot of coverage of NixOS on YouTube from my favorite Linux content creators, so I've decided to jump on the band wagon and check it out. For those that don't know, NixOS is a linux distro that revolves around the Nix package manager. The main purpose of Nix is to provide reproducible and relible builds. Basically, think Terraform but for anything happening on your Linux system. NixOS takes this to the next level by allowing the user to configure everything relating to your OS in a configuration file! This file can then be moved to another system running NixOS, run a single command, and BOOM, a system that is identical to the other system. 

Since I'm pretty particular as to how my system is partitioned and what filesystem I use, I decided to setup a LUKS-BTRFS-LVM install. I know there are libraries like [disko](https://github.com/nix-community/disko), but I've decided to go through the initial install manually to get a better grasp of NixOS.  

# Partitioning
To start off with, this is the partitioning layout I've come up with:

```
/dev/nvme0n1p1 - 600M /boot/efi partition
/dev/nvme0n1p2 - 1G /boot parition
/dev/nvme0n1p3 (LUKS)
  |_ 32GB swap LVM 
  |_ Rest of Drive root btrfs LVM
      |_ @ (root) 
      |_ @home
      |_ @nix (holds nix store)
      |_ @persist (contants system state)
      |_ @log (/var/log)
      |_ @fresh (RO snapshot of @, used to clean darlings)
```

# Setup 

Create a new LUKS Partition and open it:
```
cryptsetup luksFormat /dev/nvme0n1p3 --label CRYPT
cryptsetup open /dev/nvme0n1p3 crypt
```

Initiate the LVM structure:
```
pvcreate /dev/mapper/crypt
vgcreate vg /dev/mapper/crypt
```

Create a parition for the swap and root:
```
lvcreate -L 32G -n swap vg
lvcreate -l '100%FREE' -n root vg
```

Format the partitions:
```
mkswap -L swap /dev/vg/swap
mkfs.btrfs /dev/vg/root
```

## Btrfs

Create the subvolumes for the root partition:
```
mount /dev/vg/root /mnt

btrfs subvolume create /mnt/@
btrfs subvolume create /mnt/@home
btrfs subvolume create /mnt/@nix
btrfs subvolume create /mnt/@persist
btrfs subvolume create /mnt/@log
```

Create a Read-Only snapshot of root subvolume: 
```
btrfs subvolume snapshot -r /mnt/@ /mnt/@fresh
umount /mnt
```

Mount the partitions and subvolumes:
```
mount -o compress=zstd,subvol=@ /dev/vg/root /mnt

mkdir -p /mnt/{home,nix,persist,var/log,boot}

mount -o compress=zstd,subvol=@home /dev/vg/root /mnt/home
mount -o compress=zstd,noatime,subvol=@nix /dev/vg/root /mnt/nix
mount -o compress=zstd,subvol=@persist /dev/vg/root /mnt/persist
mount -o compress=zstd,subvol=@log /dev/vg/root /mnt/var/log

mount /dev/nvme0n1p2 /mnt/boot
mkdir -p /mnt/boot/efi
mount /dev/nvme0n1p1 /mnt/boot/efi

swapon /dev/vg/swap
```

Generate the configuration:
```
nixos-generate-config --root /mnt
```


By default, NixOS doesn’t recognize LUKS devices, so we need to add the following in the `hardware-configuration.nix`:
```
  boot.initrd.luks.devices = {
    luksroot = {
      device = "/dev/disk/by-uuid/THE_UUID_OF_THE_LUKS_PARTITION";
      preLVM = true;
      allowDiscards = true;
    };
  };
```

The mount options for the filesystems are not detected automatically by the NixOS installer, so we need to add the following:
```
  fileSystems."/" =
    { 
      options = [ "subvol=@" "compress=zstd" ]; # Options should look like this
    };

  fileSystems."/nix" =
    { 
      options = [ "subvol=@nix" "compress=zstd" "noatime" ]; # Or This
    };
```

# Installation

Finally, its time to install NixOS
```
nixos-install

reboot
```


# References
- https://hubrecht.ovh/posts/nixos-01/
- https://stackoverflow.com/questions/18042216/how-to-deactivate-a-lvm2-physical-volume-to-remove-the-drive
- https://nixos.wiki/wiki/Btrfs#Installation_with_encryption
- https://grahamc.com/blog/erase-your-darlings/
