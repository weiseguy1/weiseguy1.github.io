---
title: "AZ-900 Day 11: Monitoring and Management"
date: 2024-05-05T18:45:54-05:00
description: ""
draft: true
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/day-11/cover.png)

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

## Compliance

## Privacy

## Trust 

## Azure Arc
