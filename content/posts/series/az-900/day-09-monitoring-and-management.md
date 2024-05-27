---
title: "AZ-900 Day 09: Monitoring and Management"
date: 2024-05-15T18:45:54-05:00
description: ""
draft: true
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/day-09/cover.png)

## Introduction

How Azure allows you to apply consistent management and policies across your Azure resources, 

## Governance

### Azure Policy

Governance validates that your organization can achieve its goals through effective and efficient use of IT.

A policy is a set of rules that are used to make sure standards and agreements within your company are followed and that resources are compliant with these policies.

Role-based Access Control (RBAC)
1. Define User Access - You can define specific user access to individual resources.
2. Minimum Access - RBAC can enable minimum access necessary to resources. The ensures only users with valid access can manage resources.
3. Target Specific Use Cases - Be very explicit about uses and access. For example, allow an application access to certain resources or allow a user to manage resources in a resource group

Role Assignments have 3 elements:
Security Pricipal - An object representing an entity such as a user or group, which can access the resource.

Role Definition - A collection of premissions such as read, write and delete.

Scope - The resources the access applies to. Specify which role can access a resource or resource group

Locks
1. Assigning - Assign a lock to a subscription, resource group or resource
2. Type - A lock ca be of two types. Delete, where you can't delete the locked object. Read-Only, where you can't make any changes to the object.
3. Locked means locked - A lock needs to be removed before the locked actions can be performed again.

Azure Blueprints
Blueprints are templates for creating Azure resources.

Cloud Adoption Framework
1. A collection of documents - Lots of resources to guide you through the cloud adoption process
2. Guidance - Help to define strategies for adoption, planning the "move", "being ready" for the cloud, adoption reasons, governance pratices, and managing a cloud architecture
3. Governance - Key to the cloud adoption process in governance of the process. The Cloud Adoption Framework is a big step in that process.

Azure Advisor for Security Assistance
This is part of the Azure Security Center

Governance keeps you compliant and out of trouble
- Azure Policy ensures that polices applied to resources are compliant
- A policy is a set of rules to ensure compliant resources
- Role Based Access Control (RBAC) ensures user compliance through assigning a role to a user. A role is a combination of security principal, role definition and scope.
- Locks make sure subscriptions, resource groups or resources are either not modified or not deleted.
- Blueprints are templates for creating standard Azure environments.
- The Azure Advisor for Security Assistance is part of the Security Center.

## Azure Monitor 

Telemetry is the collection of measurements or other data at remote or inaccessible points and their automatic transmission to receiving equipment for monitoring.

1. Constant Feed - Most Azure services feed telemetry data into Azure Monitor. Even on-prem services can send telemetry data to Azure Monitor.
2. Fully Managed - Azure Monitor is centralized and fully managed. You can analyze all the data from one place.
3. Query Language - Full access to an interactive query language to learn about the telemetry data.
4. Machine Learning - Predict and recognize problems faster with built-in machine learning

## Monitoring Tools

Azure includes multiple monitoring tools to gain full visibility into your Azure environment: 
**Log Analytics**
- Azure Monitor generates A LOT of logs and telemetry data.
- Log Analytics stores and queries (or analyzes) that data to gain valuable insights.
    - Examples: VM disk size, VPN connection logs, Long term analysis, Combine metrics for complex queries.
- Choose between pre-built and custom queries
    - Queries in Kusto Query Language (KQL) format

**Application Insights**
Performance insights for web applications
Answer Questions:
- How are users using our app?
- Where are our performance bottlenecks?
- Why are we getting website errors?

Web Apps only 
Available for App Services, Azure VMs, and non-Azure resources
- VMs require installed agents

Application Insight scenario
- Find performance bottlenecks in web apps
- Discover how users are using the website

**Azure Monitor Alerts**
When something breaks, alert someone to fix it!
Notifications in response to unexpected events
- Examples: VM unresponsiveness, VM using excessive CPU, Application latency over 500 ms
Alert Components 
Alert rules
- Monitored resources
- Monitored telemetry
- Conditions to trigger alert
- Assigned severity

Rule Example:
- Monitored resource: VM
- Monitored telemetry: CPU utilization
- Condition: > 90% CPU for 5 minutes
- Severity: 2 - Warning


Action group = actions taken when rule is triggered
- Notification targets
    - Email/SMS to support personnel
    - Send to automation workflows (Logic Apps, Azure Functions, and more)

In all scenarios, when something is not working as expected, Azure Monitor alerts inform the right group to do something about it.

## Azure Service Health

Notifies you about any planned and unplanned incidents on the platform.
Maintenance - Azure needs to be updated and maintained just like any other computing infrastructure

Features:
1. Dashboard - A personalized dashboard to highlight service issues affecting your resources.
2. Custom Alerts - Get notified of planned and non-planned outages. Alerts are simple to set up and customize
3. Real-Time Tracking - Track any alerts and issues in real-time and get full reports once resolved.
4. Free Service - The Azure Service Health service is completely free.

## Compliance

Scenario - Europe
If companies within the EU don't take compliance seriously, they can face massive fines.

Industry Regulations
- General Data Protection Regulation - Main objective is to protect individuals and processing of their data. It gives control of personal data back to the individual, instead of the company owning it. Companies are required to implement a lot of tools for consumers to control their data.
- ISO Standard - Many different ISO categories, such as compliance with quality and customer satisfaction. Most common ISO 9001:2008. Also includes food safety and environmental management.
- NIST - National Institute of Standards and Technology. Focuses purely on the tech industry. Developed primarily for US Federal agencies. Compliance with NIST means compliance with multiple Federal US regulations.

Azure Compliance Manager - Azure knows about compliance and resources, and can give you recommendations through the Compliance Manager.
Benefits:
- Recommendations - Get recommendations for ensuring compliance with GDPR, ISO, NIST and others.
- Tasks - Assign compliance tasks to team members and track progress
- Compliance Score - Chase a perfect score to be 100% compliant
- Secure Storage - Upload documents to prove compliance and store them security.
- Reports - Get reports of compliance data to provide to managers and auditors. 

Azure Goverment Cloud
- Dedicated Regions - If you are a US govermenment body or contract for one, you can get access. The Goverment Cloud consists of dedicated separate datacenters.
- Exclusivity - You are guaranteed only screened personnel from US federal, state and local government have access
- Compliance - Ensure compliance with required US government agencies, and level 5 Department of Defense approval.
- Azure Benefits - You get standard Azure cloud Benefits: high availability, scalability and managed resources.

China Region
- Located in China - Azure datacenter is physically located within China and has no connection outside of China, including other Azure regions.
- Data is Kept in China - All customer data is kept inside Chinese borders. Certain global Azure services won't work fully.
- Compliant - You are ensured compliance with Chinese regulations at all times.

## Privacy

1. Azure Information Protection - Classify label and protect data based on data sensitivity
2. Azure Policy - Define and enforce rules to ensure privacy and external regulations.
3. Guides - Use guides on Azure to respond and comply with GDPR privacy requests.
4. Compliance Manager - Make sure you are following privacy guidelines.

## Trust 

Trust Center and Service Trust Portal
- Trust Center - Learn about Microsoft's effort on security, privacy, GDPR, data location, compliance and more. A hub for more information about trust in each product and service.
- Service Trust Portal - Review all the independent reports and audits performed on Microsoft's products and services.

## Azure Arc

The Challenge of Managing Complex Environments. Computing resources in multiple locations (i.e., Azure, On-Prem, Other Clouds). Each computing sources uses its own management tools. More locations means more management overhead. Also, cannot apply Azure governance polices to non-Azure resources. This is where Azure Arc comes in as it allows management of both Azure and non-Azure resources as well as apply Azure governance polices to non-Azure resources in the same interface. 

The technical definition of Azure Arc is:
> Centralized governance and management on on-prem and multi-cloud computing resources.
In short, Azure Arc manages non-Azure resources as if they were in Azure by extending Azure cloud management and services to them. Azure Arc works by installing agents on non-Azure resources that bring them into Azures control plane. 

Benefits:
1. Manage Azure and non-Azure resources in the same place
2. Manage non-Azure Kubernetes clusters
3. Deploy Azure-managed database services to non-Azure locations
4. Manage and protect non-Azure servers. Monitor non-Azure OSs alongside Azure VMs. Protect with Microsoft Defender for Cloud. Apply Azure Automation runbooks.
5. Apply Azure governance. (RBAC, Azure Policies, Azure Blueprints)
6. Deploy Azure serverless services to non-Azure hardware (Azure App Service, Azure Functions, Azure Logic Apps)
