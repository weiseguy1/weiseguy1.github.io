---
title: "AZ-900 Day 01: Introduction"
date: 2024-04-21T15:11:22-05:00
description: "The foundational information for the AZ-900"
draft: false 
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/day-01/cover.png)

## Introduction
In today's IT infrastructure, it is more than likely that you will run into Cloud technologies in your workplace. Cloud allows for companies to save money by reducing operating cost and off-loading the cost of physical servers to the cloud provider. In this series, I'll be covering information for the AZ-900, the entry level certification for Microsoft's cloud provider, Azure. 

The AZ-900 covers the basics of what every Azure Cloud Administrator should know. According to Microsoft's Official Study Guide [^1], the exam covers topics:
- Describe cloud concepts (25–30%)
    - Describe cloud computing
    - Describe the benefits of using cloud services
    - Describe cloud service types
- Describe Azure architecture and services (35–40%)
    - Describe the core architectural components of Azure
    - Describe Azure compute and networking services
    - Describe Azure storage services
    - Describe Azure identity, access, and security
- Describe Azure management and governance (30–35%)
    - Describe cost management in Azure
    - Describe features and tools in Azure for governance and compliance
    - Describe features and tools for managing and deploying Azure resources
    - Describe monitoring tools in Azure

In this post, we'll cover some basic introductory knowledge, like:
- Azure Portal [^2]
- Azure Command Lines [^2]
    - Azure CLI
    - Azure Powershell
    - Azure Cloud Shell
- ARM Templates [^3]
- Azure Advisor [^4]


## Azure Portal
To start, we'll go over what you'll be engaging with on a regular basis, the Azure Portal.    

![Azure Portal](/images/posts/series/az-900/day-01/image-1.png)

This is the web front end where you will manually interact with any of the Azure Services. Not only that, but the portal allows for some customization with personal dashboards, layouts, workflows and the like. You will also use the portal to engage with Access Controls, Cost Management and to get updates on the platform.

To access the Azure Portal, you'll need to have a Microsoft Account and then go to [portal.azure.com](https://azure.microsoft.com/en-us/free) to register for an account. Its here that you'll have the option to try some popular Azure Services for free up to 12 months and get a $200 credit for 30 days. You can even access the Azure Portal from your phone using the Android or iOS app. Here you can do most of what you can do through the web interface. Go ahead and try it out!

## Azure Command Lines
Next up, there are the command lines that accompany Azure. The command lines shown here allow an Adminstrator or Developer to interact with Azure without having to the mess around with web interface. These include:
- Azure CLI
- Azure Powershell
- Azure Cloud Shell

Azure CLI and Azure Powershell are a command line interfaces that is used to interact with Azure. The main difference between the two is Azure CLI is written in Bash, whereas Azure Powershell uses Powershell cmdlets. Both CLIs are cross platform and can be installed on Windows, Linux or Mac. With these tools, you can do simple one time changes to your Azure infrastructure, or you can combine commands together to perform more complex actions in an automated fashion. This allows for a sense of structure in how your resources are managed. 

The final CLI that needs to be talked about is Azure Cloud Shell. This shell is different as it is not something that can be installed locally. As the name implies, it is a shell that is available in the cloud. This is nice as the Cloud Shell is then available anywhere you have an internet connection, on any device. In the Cloud Shell, you can use either Azure Powershell or Azure CLI to complete your task. It also uses your credentials from logging into Azure to determine your permissions.  

## ARM Templates

Azure Resource Manager or ARM for short, is the deployment and management server for Azure. Everything you do in Azure has to go though ARM as it is responsible for creating, updating, and deleting resources on the platform. The way ARM works is, you send Azure a request, ARM takes that request and makes sure that you are both authenticated and authorized to perform that task. ARM then sends the requested action to the specific Azure Service, where it is then processed. The reason why ARM does this is that it makes the results consistent, regardless of what you are using to engage with Azure.

ARM Templates, on the other hand, are templates written in a JSON format that can be used to manage your infrastructure rather than using scripts. By doing this, you can manage your resources in a declaritive and repeatable manager. You can even break down the templates into smaller individual templates to be reused in larger deployments. Also, you can add Azure Powershell or Azure CLI scripts inside the templates or have them called as external programs to make deployments easier and more extensibile. 

## Azure Advisor

Azure Advisor takes note of your entire Azure environment and then makes suggestions. As to what Azure Advisor suggests, it gives you recommendations in five categories:
- **Reliability** which is used to make sure the longevity of your business-critical services. 
- **Security** which covers threats and vulnerabilities.
- **Performance** which improves speed of the application.
- **Operational Excellence** which covers workflow efficiency, resource management, and best practices for deployments.
- **Cost** which can help reduce your overall Azure spending.

Azure Advisor is automatically turned on, but can be managed by search for "Advisor" in the search bar in Azure or can be accessed from the left hand hamburger menu. See the image below. 
![Azure Advisor](/images/posts/series/az-900/day-01/image-2.png)

## Wrapping it up

That's a lot of studying for one day! In today's article we've covered what the Azure Portal, Azure Command Lines, ARM Templates, Azure Advisor are. When you have some time, please check out these services on your own to get some hands on experience. If you've enjoyed this post, please feel free to check out the other articles on my site. In the next post of this series, we'll go over cloud concepts which are important to know for the AZ-900. Stay tuned! 

## References
[^1]: https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/az-900
[^2]: https://learn.microsoft.com/en-us/training/modules/describe-features-tools-manage-deploy-azure-resources/2-describe-interacting-azure
[^3]: https://learn.microsoft.com/en-us/training/modules/describe-features-tools-manage-deploy-azure-resources/4-describe-azure-resource-manager-azure-arm-templates
[^4]: https://learn.microsoft.com/en-us/training/modules/describe-monitoring-tools-azure/2-describe-purpose-of-azure-advisor
