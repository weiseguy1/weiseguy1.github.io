---
title: "Learning Devops (Day 03): Packer"
date: 2024-07-17T21:26:28-05:00
description: ""
draft: true
type: "post"
tags: ["series", "devops", "packer"]
showTableOfContents: true
---

![Cover Image](/images/posts/series/learning-devops/day-03/cover.png)

## Introduction
Hey everyone, welcome again to this series on Learning DevOps. In this post I will be going over Packer, an open source image creation tool from HashiCorp. We will be using Packer to help generate what are known as *"Golden Images"* on Azure and then use these images to spin up a fresh VM with our custom configuration options applied ready to go. If this sounds good to you, then lets get started with Packer.

## Packer

So you might be wondering, *"What is Packer? And why is it useful?"*. If you asked yourself this, then I can't blame you. To answer the first question of, *"What is Packer?"*, then to put it simply, Packer is a tool from HashiCorp that uses configuration files written in *HashiCorp Configuration Language* (HCL) or JSON to create identical images for multiple platforms. These platforms could range from cloud platforms like Azure, AWS and GCP to creating local VM images in Proxmox, VMWare ESXI, or even VirtualBox. 

To answer the second question as to, *"Why is it useful?"*. Packer creates identical VM images from a single configuration file. This is useful for reproducability and standardization. If your company has to follow a certain policies or regulations like [NIST](https://www.nist.gov/cybersecurity) or the [GDPR](https://gdpr-info.eu/), Packer can be used to configure your VM images, both Windows and Linux, to follow these standards in an automated way. You can even add Packer to your CI/CD pipeline for a fully automated VM image experience. 

To install Packer for your specific operating system, you can go to the [Packer.io install](https://developer.hashicorp.com/packer/install) page. There you can find instructions on how to install the latest version of Packer for Mac, Windows and Linux. 

### HCL or JSON

As stated earlier, you have your choice of writing your Packer configuration in either HCL or JSON. The differences are:

 | JSON | HCL |
 | --- | --- |
 | The initial configuration language of Packer | HashiCorps own configuration language added in v1.5.0 |
 | Recognizable syntax | Slight learning curve | 
 | No easy way to add comments | Comment support |
 | Harder to read | Easier to read |

With this in mind, I personally like HCL as it is easier to read. If you've read my post on [Terraform](/posts/series/learning-devops/day-01-terraform/), then you've worked with HCL. Also, HCL integrates better with HashiCorp products (Suprise, or not :grin: ). 

## Wrapping it up


