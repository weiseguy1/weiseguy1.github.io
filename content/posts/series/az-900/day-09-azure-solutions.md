---
title: "AZ-900 Day 09: Azure Solutions"
date: 2024-05-03T18:45:30-05:00
description: "More supplemental content, but informative"
draft: true
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/day-09/cover.png)

## Internet of Things

A system of interrelated computing devices, mechanical and digital machines, objects, animals or people that are provided with unique identifiers and the ability to transfer data over a network without requiring human-to-human or human-to-computer interactions.

### IoT Hub
- Features
	- Managed and Secure
	- Ease of Deployment
	- Platform-as-a-Service

### IoT Central
1. Application Platform as a Service (aPaaS) - Simply and speed up the implementation of your IoT solution.
2. No Coding Needed - You don't have to know how to write code to deploy your IoT project. Receive feeds from devices and focus on metrics and business value.
3. Pre-made Containers - Use any of the hundreds of connectors that are ready to use in IoT Central.

### Azure Sphere
An all-in-one solution for IoT devices on Azure

- Specific Hardware - You can only use hardware and chipsets certified by Microsoft for use in Azure.
- Security - Specialized security service that manages maintenance, updates and general control
- Operating System - Custom made for Azure Sphere devices. Connects to the Sphere Security Service.


### Solutions 
- IoT Hub - PaaS solution that provides more control over the IoT data collection and processing
- IoT Central - aPaaS solution that providers pre-made IoT connections and dashboards to get setup quickly.

## Big Data

### Moving Definition
- Data from Millions of Devices
- The definition of how big "Big Data" is changes as the industry can process more and more data

### Business Value
- Big Data = Better service, Better products, More profits
### Data Lake Analytics
1. Large Amounts of Data - A data lake is a very large body of data
2. Parallel Processing - Two or more processes or computers processing the same data at the same time. Data Lake Analytics includes parallel processing 
3. Ready to Go - Servers, processes and any other needed services are ready to go from the start. Jump straight into the data analytics

### HDInsights
- Similar to Azure Data Lake Analytics
- Open Source, which is free and community supported
- Includes Apache Hadoop, Spark and Kafka

### Azure Databricks
- Based on Apache Spark, a distributed cluster-computing framework.
- Run and process a dataset on many computers simultaneously
- Databricks provides all the computing power 
- Integrates with other Azure Storage services

### Azure Synapse Analytics
- Azure's data warehouse offering
- Used to be called Azure SQL Data Warehouse
- Used for reporting and data analysis
- Only limited by your scope
- Use Synapse SQL language to manipulate the data

### Outcomes 
- Speed - Speed and efficiency of processing large amounts of data, provides real value
- Cost Reduction - Save large amounts of money on storage and processing, by using a Big Data solution in the cloud
- Better Decision Making - Immediate data processing and analysis in-memory means you can make better decisions, and make them faster
- New Products and Services - Understand what customers want and provide them with much better products and services

## Machine Learning

AI is the capability of a machine to imitate intelligent human behavior. Through AI, machines can analyse images, comprehend speech, interact in natural ways and make predictions using data

### Machine Learning/AI
1. Models - The definition of what your machine learning application is learning. A model is a set of rules of how to use the data provided. The model finds patterns based on the rules.
2. Knowledge Mining - Use Azure Search to finding existing insights in your data. File relationships, geography connections and more.
3. Built-in Apps - Azure has a number of built-in apps that you can use for machine learning and AI straight away. These include cognitive services and bot services.

### Azure Bot Service
Azure PaaS offering that lets you build bots for Q&A services, virtual assistants and more. 
- Code or Visual - Create a bot using the visual editor or programming
- Language - Let users talk to your bot with natural language and speech integration
- Integration - Integrate the bot with other services, like Facebook Messenger, Teams, Twillo and more. 
- Branding - Use your own branding and own the data the bot uses and produces.

### Azure Cognitive Services
1. Vision - you can use the vision service to recognize, identify and caption your videos and images. Automatically
2. Decision - Apps can make decisions based on content. Detect potential offensive language, detect IoT anomalies and leverage data analytics
3. Speech - Automatic speech-to-text translation, Speaker identification and verification

### Azure Machine Learning Studio
- Supports all Azure Machine Learning tools.
- Pre-made modules for your project
- Use for real-world scenarios, such as Twitter sentiment analysis, photo grouping and movie recommendations.

### Machine Learning Service
1. End-to-End Service - The service to use AI and machine learning almost anywhere on Azure
2. Tooling - The Machine Learning Service is a collection of tools to help you build AI applications
3. Automation - Azure automatically recognizes trends in your applications and creates models for you.

## Serverless

### Azure Functions
1. Golden Oldie - It is the first "serverless" service on Azure. The Azure service most will start with when exploring serverless architecture
2. Single Task - It is called function as only a single task is performed every time. The function only runs once for each invocation
3. Basic Compute Unit - It is a fundamental compute action and can be run millions of times per second if needed

### Logic Apps
- Connect Systems - Connect systems both inside and outside of the Azure platform. Integrate not only apps, but also data flows, services and entire systems.
- Automation - A lot of ways to schedule, automate and orchestrate tasks and processes.
- Quick Start - No coding required to get started straight away. You just need access to your apps to integrate.

### Azure Event Grid
1. Routing Service - Event Grid is a routing service for sending and receiving events between applications.
2. Serverless - No management of infrastructure components. Create an Azure Event Grid and start connecting services
3. Ease of Use - Event Grid Makes complex cloud architecture simpler

Serverless approaches work extremely well with cloud services. ACG is all serverless.
- Yes, there are servers (they just aren't yours)
- Azure Functions are the most basic compute tasks. Does one function then dies until next time it is called.
- Logic Apps are a quick and simple way to integrate systems and applications inside and outside of Azure.
- Event Grid is a routing service for passing events between applications that need to know about the events

## DevOps

DevOps is the work between development and production

DevOps is at its core about people: how developers, engineers and system administrators organize themselves and work as a team to deliver better products faster

### Azure DevOps
- Azure Boards - Keeps track of work tasks, timelines, issues, planning and much more.
- Azure Pipelines - Produce and test your software automatically and continuously
- Azure Repos - Store source code for your application securely in a managed way.
- Azure Test Plans - Design tests of applications to implement automatically.
- Azure Artifacts - Share applications and code libraries with other teams inside or outside your organization

### Azure DevTest Labs
1. Environment Management - Allow developers and engineers to create environments for test and development
2. Cost Management - You won't incur unexpected costs and will even minimize waste of resources on your account
3. Templates - Tailor your development and test environments and reuse them with templated deployments.

### Github and Github Actions

##### Github
- Acquired in 2018 by Microsoft
- Code repository service for lots of bit and small projects
- A favorite among open-source communities
- Microsoft themselves are one of the biggest users of Github
##### Github Actions
- Very similar to Azure Pipelines.
- Build, test and publish code
- Works with almost any platform, such as AWS, GCP and many more
