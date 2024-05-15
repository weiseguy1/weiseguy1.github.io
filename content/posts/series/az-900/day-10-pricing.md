---
title: "AZ-900 Day 10: Pricing"
date: 2024-05-06T18:46:09-05:00
description: ""
draft: true
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/day-10/cover.png)

## Introduction

Pricing Structure
| On-Prem | Azure |
| --- | --- |
| Utilization is well below 100% | You don't own the hardware |
| No monthly costs | Pay for number of hours you use. |
| Large upfront cost | Pay more for more resources. |
| Pay for utilities | Service payment is tiered |
| N/A | Location can affect price | 

## Subscriptions

Billing & Pricing - All resources belong to a subscription

1. Multiple Subscriptions - Any Azure account can have multiple subscriptions. Useful for organizing who pays for what
2. Billing Admin - One or more users can be a "billing admin", which manages anything to do with billing and invoicing on Azure. Ensures separation of responsibility.
3. Billing Cycle - A billing cycle on Azure is either 30 or 60 days

Offer types - the type of subscription. There are many different ones at any one time.

Management Groups
- Group Subscriptions - Take action across subscriptions in bulk. Very useful in large organizations with many subscriptions. 
- Organize - Manage access, policies and compliance in bulk. E.g. have a management group per country or department. 
- Billing Logic - You maintain the billing associated with the right budgets. Nest management groups to indicated hierarchy and relationship.

## Cost Management

Buying Azure Services - You can't use Azure without buying services and products. 

Free Accounts
1. Truely Free
2. Benefits
3. Always Free Services 

Azure Cost Management
- Azure Portal - Access the Azure Cost Management tool from within the Azure Portal. Get a detailed view of current and projected costs. Azure Cost Management is free and included within all Azure subscriptions
- Report & Recommendations - Get detailed spending reports and recommendations on how to save on costs and analyze them.
- Optimization - Optimize your current resources to save money and monitor any Amazon Web Services charges too.

Spot VM Usage - You can save up to 90% off the price by choosing to use a Spot VM. They are not guaranteed they will run forever as Azure can evict you anytime they need the compute capacity back.

## Pricing Factors

Calculating Azure costs on mature infrastructure is almost impossible

Influences on Pricing
- Resource Size - Different sizes of resources will have different pricing. A more powerful virtual machine will cost more.
- Resource Type - There is a very big difference in the amount of hardware resources needed for various types of resources, as well as complexity.
- Location - Different Azure locations have different prices for services. Exchange rates, labor costs and more have an influence on the price.
- Bandwidth - The bandwidth your services are using incurs a cost as well. 
Azure has 3 billing zones with contain many regions. Any data transfer within a single billing zone (ingress) is free but any data transfer between billing zones (egress) will incur a cost.

Pricing Calculator
Choose from all available Azure Services.
Select resource properties such as for a VM
Monthly cost estimate
Export estimate for further analysis and use

Total Cost of Ownership Calculator
Get an estimate of the total savings you could get for moving your on-prem resources to Azure. Estimate total savings over a period of time by using Azure. Comprehensive reports to share with stakeholders

## Best Practices

Spending Limits
1. Default Limit - Some Azure accounts with monthly credits to use will have a default spending limit. When the credits are used, the limit kicks in. 
2. No Increase - When the credits are gone, either remove the limit entirely or leave it in effect.
3. No Spending Limit - Pay-as-you-go accounts have no spending limit functionalilty.

Quotas
- Property Limit - A quota is a limit on a certain property of an Azure service. For example, a maxmimum of 100 namespaces for Event Hub.
- Ensure Service Level - The quotas are necessary to ensure Azure can maintain their high service level
- Quota Change - if you need to increase the quota for a particular service, you can ask Microsoft to increase them.

Tags - Non-functional labels that are attached to resources or resource groups and you can use as many tags as you want.
Best Practices
- Identify Roles - Protect sensitive data by defining which roles can access a resource
- Related Resources - To make bulk processing and updating easier, define which resources are related
- Filter - Filter resources per project, customer or for reporting purposes
- Unambiguous - Create a list of tags used that includes: description, tag name, and potential values.

Pay-as-you-go is the most expensive as you are paying a non-commit premium to use the services 
Reserved Instances can save you money as you are commited to use the resources for an extended period of time. However, not all Azure services can be reserved.

Reserved Capacity
Azure will reserve capacity of Azure SQL (save 80%), Cosmos DB (save 65%), Synapse Analytics (save 65%), or Redis Cache (save 55%) for a 1- or 3-year commitment. Change regions, scale up or down, apply it to multiple subscriptions, and cancel at any time.

Azure Hybrid Benefit - Use existing licenses of products to save costs when using Azure

Advisor Portal gives you best practice advice in general through recommendations.
