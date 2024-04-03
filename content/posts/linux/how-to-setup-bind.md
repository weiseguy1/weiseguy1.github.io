---
title: "How to Setup Bind"
date: 2024-03-30T22:29:08-05:00
description: "A short tutorial on local DNS"
draft: true
type: "post"
tags: ["linux", "dns", "administration"]
showTableOfContents: true
---

![2FA on SSH](/images/posts/linux/how-to-setup-bind9/setupBind9.png)

## Introduction

Domain Name System or as commonly called DNS, is a way for computers to translate an IP address to a Fully Qualified Domain Name (FQDN). In simple terms, if you wanted to go to say `kernel.org`, you would just need to type that into your browser instead of typing `139.178.84.217` for the IPv4 address. Or if you wanted to be a bit more extra, here is `kernel.org`'s IPv6 address: `2604:1380:4641:c500::1`. Commonly referred to as the internets dictionary, DNS is extremely helpful by giving meaningful names to otherwise complicated output.   

It is important to have a cursory knowledge on DNS and how it works. The best way to truely learn is to actually set up a DNS server and test it out. For most business networks, DNS is a crucial part of the daily functionings as it is used not only for easily allowing customers to find their sites, but it also is used in other programs like Active Directory or LDAP.  

In this guide, I'll be showing how to manually setup bind9 servers (a primary and secondary) on 2 Debian 12 VMs. *I may in another article write how to setup bind9 using Ansible in the future. Keep a lookout for that :)*

### Prerequisites

To follow along with this guide, you'll need:

- 2x Debian Servers (1GB of RAM and 1 CPU per)

## Setup the Debian Servers

To start, I'll be going over how to install a bare install of Debian 12 in a VM. Go ahead and use whatever VM software you feel comfortable with. For me, I'm going to be using `virt-manager` as I just like `qemu/kvm`. 

The first thing you're going to need to do is download the debian iso from their [downloads page](https://www.debian.org/download). 

