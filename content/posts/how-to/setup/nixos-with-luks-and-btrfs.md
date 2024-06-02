---
title: "How to Setup NixOS with LUKS and BTRFS"
date: 2024-05-30T06:02:02-05:00
description: "A BTR-y smooth installation"
draft: true
type: "post"
tags: ["nixos", "how-to", "linux"]
showTableOfContents: true
---

![Cover Image](/images/posts/how-to/setup/nixos-with-luks-and-btrfs/cover.png)

# Introduction


# Partitioning
```
/dev/sda1 - 815MiB EFI partition
/dev/sda2 (LUKS)
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
cryptsetup luksFormat /dev/sda2 --label CRYPT
cryptsetup open /dev/sda2 crypt
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
```



lvchange -an <lvpath>
vgchange -an <vgname>

# References
- https://hubrecht.ovh/posts/nixos-01/
- https://stackoverflow.com/questions/18042216/how-to-deactivate-a-lvm2-physical-volume-to-remove-the-drive
- https://nixos.wiki/wiki/Btrfs#Installation_with_encryption
- https://grahamc.com/blog/erase-your-darlings/
