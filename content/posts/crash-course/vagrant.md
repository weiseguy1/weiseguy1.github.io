---
title: "Vagrant Crash Course"
date: 2024-04-30T18:44:03-05:00
description: "An Introduction into Virtualization Automation"
draft: true
type: "post"
tags: ["vagrant", "devops", "virtualization", "crash course"]
showTableOfContents: true
---

![Cover Art](/images/posts/crash-course/vagrant/cover.png)

# Introduction

In today's world of IT automation, it might be hard to choose which tool you should learn first. Should you start with provisioning using Ansible, Chef or Puppet? Or, how about starting out with the heavy-hitter and learn Terraform or OpenTofu? In reality it comes down as to where you want to focus the most. 

I have already did multiple articles on [Docker](/tags/docker) and decided that the next tool that would be great to learn is [Vagrant](https://www.vagrantup.com/). But, what is vagrant? What is its use case? And, how can it help me at work? All of these questions and more will be answered through out this crash course. So, let's buckle up and let's get started!

## What is Virtualization?

To fully understand what Vagrant does, we first have to know what virtualization is. So, according to AWS:
> Virtualization is technology that you can use to create virtual representations of servers, storage, networks, and other physical machines.

This means we can take a single machine, in this case your laptop or desktop, to create as many virtual machines, also known as guest operating systems, as your system can allow. In other words, think of your machine as a box, every time you create a virtual machine or VM, you would then be placing a smaller box inside of the large one very similar to what this image below shows. 


![VM boxes](/images/posts/crash-course/vagrant/image-1.png)

## What is a Hypervisor?

Ok, so a VM is a virtualized instance of an OS that can run on your machine. But, how is the VM made? This is done through a piece of software known as a Hypervisor. A Hypervisor comes to 2 different types:
- Type I Hypervisor: A hypervisor that runs bare metal on the host without an underlying operating system
![Type I Hypervisor](/images/posts/crash-course/vagrant/image-2.png)
***Examples: Hyper-V, VMware Esxi, Proxmox VE***

- Type II Hypervisor: A hypervisor that runs on top of the operating system as a service or process 
![Type I Hypervisor](/images/posts/crash-course/vagrant/image-3.png)
***Examples: Oracle Virtualbox, VMware Workstation, Parallels Desktop***


## What is Vagrant?

Vagrant is an automation tool, written in Ruby, that wraps around virtualization technologies and helps manage our development environment workflow. The configuration of such environments is done through files called a `Vagrantfile`, which can be shared to replicate instances. 
![Vagrant in the stack](/images/posts/crash-course/vagrant/image-4.png)

You can install Vagrant by going to [vagrantup](https://developer.hashicorp.com/vagrant/install) and install it based on your operating system.

## Plugins

Vagrant uses Virtualbox as the default provider to manage your VMs. It also ships with support for other hypervisors such as VMware Workstation, Hyper-V and even Docker. However, if your run Linux like me and like to use QEMU/KVM as your hypervisor of choice, then you are going to need to install a plugin to get vagrant to work properly. 

| Command | Description |
| --- | --- |
| vagrant plugin install <plugin> | Install the defined plugin |
| vagrant plugin update <plugin> | Update the defined plugin |
| vagrant plugin repair | Repair failing plugins |
| vagrant plugin license <license_file> | Add license to the proprietary plugin |
| vagrant plugin uninstall <plugin> | Removes the plugin |
| vagrant plugin expunge | Removes all plugins, dependencies, and metadata | 



## References
https://aws.amazon.com/what-is/virtualization/
