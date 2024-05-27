---
title: "AZ-900 Day 08: Security"
date: 2024-05-12T18:45:40-05:00
description: ""
draft: true
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/day-08/cover.png)

## Defense in Depth

On-Prem Defense
1. Physical Hardware - You are responsible for the security of the hardware, buildings and staff
2. Layers of Defense - You will have several layers of defense, as with a castle, such as swipe cards, security guards, firewalls and more
3. It is up to you - You own the infrastructure, so you are responsible for adequate defense of hardware and data

Azure
- Physical
- Identity and Access
- Perimeter
- Network
- Compute
- Gateways and Firewalls
- Data
## Securing Network Connectivity

### Firewall
1. Rules - A firewall defines rules for what kind of traffic can and cannot access the device or service behind it
2. Variations - Firewalls comes as hardware and software versions. They can suit any type and size of network
3. Critical Part - Any network that take security seriously will have a firewall

### DDoS
- U.S. Banks - In 2012, 6 U.S. banks were flooded with 60Gb of traffic every second
- CloudFlare - In 2014, CloudFlare was attacked with 400Gb of traffic every second
- GitHub - In 2018, GitHub experienced 1.35Tb of traffic per second. A new record of DDoS attacks.

### DDoS Protection Service
1. Many Internet-Connected Devices - A lot of computers and other connected devices target a single website to make it stop. Github had a 127M requests per second attack
2. Protection - Detects the DDoS attack and deflects it. Various levels of protection depending on scenario.
3. No Downtime - There is no interruption to your service at all. Azure will mitigate the attack policy

### Network Security Groups (NSG)
1. Resource Firewall - Personal resource firewall. Attach to virtual network, subnet or network interface.
2. Rules - A NSG determines who can access the resources attached to it, using rules for inbound and outbound traffic

### Application Security Groups
1. Protects Application Infrastructure - Focus the security on the application rather than the IP endpoint
2. Natural Extension - Group VMs and virtual networks into logical application groups and apply an application security group

## Public and Private Endpoints

### Public Endpoints = Publicly Reachable PaaS Services
Default: Managed (PaaS) services reachable over the public internet
- Virtual network -> PaaS over the public internet
- Also exposed to the public
- Problem with sensitive resources
What if we want to limit or remove public exposure?
Solution: Two available solutions: "Good" and "Better"
- Good = service endpoints
- Better = private endpoints

### Service Enpoints
Privately connect VNet subnet to Azure PaaS services
- Direct connection from subnet to Azure PaaS services
- Connects over Microsoft's private backbone (not over public internet)

Configure service to only allow traffic fro service endpoint-enabled subnet
- Can also restrict access to specific public IP addresses

Limitations of Service Endpoints
- Secure access to VNets only
	- No private on-prem access
	- Must allow on-prem access over Public IP
- PaaS public endpoint still exists
	- Not truly private
- Service endpoints provide access to an entire service
	- For example, provides private access to all of Azure Storage, not just a single storage account

### Private Endpoints
Managed network interface
- Private connection to specific instance of a service
- e.g., single storage account, SQL instance, etc.
Available over connected networks
- Hybrid/on-prem networks
- Peered virtual networks
Can completely disable public access to a connected service
- Truly private
- Public endpoint disabled
## Microsoft Defender for Cloud

### Overview
- It provides threat alerts
- It's ready for hybrid architectures
- Each VM has an agent installed that sends data
- Azure analyzes the data and alerts you if necessary

### Highlights
- Policy and compliance metrics
- A secure store to encourage great security hygiene
- Integrate with other cloud providers (requires Azure Arc)
- Alerts for resources that aren't secure

### Using Defender for Cloud
1. Define Policies - Set up policies for Azure to monitor resources from. A policy is a set of rules used to evaluate a resource. Use predefined policies or create your own
2. Protect Resources - Actively protect your resources through monitoring your policies and their outcomes
3. Respond - Respond to any security alerts. Investigate all of them, and then go back to setup 1. to define new policies to account for the alert.

## Azure Key Vault

1. Secure Hardware - The Key Vault hardware is secure too. Not even Microsoft can access the keys in it.
2. Application Isolation - An application can't pass on secrets, nor access another application's secrets
3. Global Scaling - Scale globally like any other managed Azure service

## Azure Information Protection

### Azure Information Protection
Secure documents, emails and data outside of the company network
- Classify Data - Classify data according to how sensitive it is either using policies, or manually.
- Track Activities - Track what is happening with shared data and revoke access if needed
- Share Data - Safely share data as you can control who edits, views, prints and forwards its
- Integration - Controls for document access is integrated with common applications and tools, such as Microsoft Office

## Azure Sentinel

Sentinel is a security information and event management (SIEM) tool
1. Data Collection
2. Aggregation and Normalization
3. Analysis and Threat Detection
4. Things happen (Mostly Magic)
5. Take Action

### Benefits and Features
- Behavioral Analysis - Sentinel uses AI to learn if any detected behavior is unusual
- AWS Integration - Data from AWS services can be fed directly into Sentinel. This gives you one approach for threat detection across your multi-cloud infrastructure
- Cloud Scale - Sentinel can take advantage of the Azure cloud scale and deliver more accurate results fast.

## Azure Dedicated Hosts

### Dedicated Hosts
1. Hardware Control - You get control of an entire physical server on Azure
2. Yours and Yours Alone - Physical layer isolation means you won't get any "foreign" VMs on your dedicated host.
3. Maintenance - Reduce impact on your system by choosing when to install updates to your dedicated host.

### Cloud Benefits
1. Compliance - Take advantage of the stringent Azure compliance in combination with managing your own hardware
2. Global Infrastructure - Availability zones, fault isolation, high availability and scale sets come as standard. No optional extras here
3. OS of Your Choice - Choose Windows, Linux or SQL server on a range of VM sizes. Even save money by using your own licenses

## Microsoft Defender for Identity

You really can't trust users

1. Monitor Users - Analyze user activity and information. This includes any permissions and memberships of groups
2. Baseline Behavior - Record what a user's normal behavior and routine is. Any activity outside this routine will be logged as suspicious
3. Suggest Changes - Microsoft Defender for Identity will suggest changes to conform with security best practices in order to reduce risks

### Cyber-Attack Kill Chain
1. Reconnaissance - If a user is searching for information about other users, device IP addresses and more, Microsoft Defender of Identity will raise alerts
2. Brute Force - Any attempts to guess user creds will be identified and flagged
3. Increasing Privileges - Any attempt by a user to gain more privileges will be flagged. This could be through another user's login
