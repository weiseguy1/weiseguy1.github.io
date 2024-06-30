---
title: "How to Fix Networking in Proxmox"
date: 2024-06-29T19:48:03-05:00
description: "Fixing Guest OS networking in Proxmox"
draft: false
type: "post"
tags: ["networking", "homelab", "troubleshooting"]
showTableOfContents: true
---

![Cover Image](/images/posts/how-to/fix/networking-in-proxmox/cover.png)

## Introduction

When initially setting up Proxmox, I ran into an issue where my Windows Server guest OS couldn't access my local network or even the internet. The host worked just fine and I was able to run a ping to Cloudflare DNS servers. So, I decided to look at the way networking was setup in Proxmox.

**Default /etc/network/interfaces**

```
auto lo
iface lo inet loopback

iface enp5s0 inet manual

auto vmbr0
iface vmbr0 inet static
        address 192.168.1.6/24
        gateway 192.168.1.1
        bridge-ports enp5s0
        bridge-stp off
        bridge-fd 0
```

It seemed the file was missing the `network` option which tells the bridge what subnet it belongs to. I just added that option below the `gateway` option, rebooted Proxmox and I had networking again. 

**Updated /etc/network/interfaces**

```
auto lo
iface lo inet loopback

iface enp5s0 inet manual

auto vmbr0
iface vmbr0 inet static
        address 192.168.1.6/24
        gateway 192.168.1.1
        network 192.168.1.0
        bridge-ports enp5s0
        bridge-stp off
        bridge-fd 0
```

## References

- https://forum.proxmox.com/threads/no-internet-access-for-vms.76261/
