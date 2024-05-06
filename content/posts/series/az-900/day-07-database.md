---
title: "AZ-900 Day 07: Databases"
date: 2024-05-05T18:44:47-05:00
description: "Supplemental for the exam, but still good to know"
draft: true
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/azure-series-day-07-database.png)

## Cosmos DB
Synchronization 
1. Easy with Cosmos - Traditional databases that weren't cloud enabled could be very difficult to set up across multiple regions. Azure takes care of all of it with Cosmos
2. One Click to Add Regions - It is very easy to expand to more regions with Cosmos DB and have the data stay in sync.
3. Continued Synchronization - Cosmos DB stays on top of all reads and writes to your data and makes sure data is moved between regions to stay in sync.

Latency - The time it takes for data to travel from one point to another

Scalability
1. Automated - Cosmos DB automatically scales to meet resource demand.
2. Infinite Resources - Any number of users of your application can be supported
3. Lowest Price - Even though the scaling is automatic, you only pay for the resources you use.

Connectivity
- Developer - Choose from various software development kits (SDKs) and appliation programming interfaces (APIs).
- Languages - A language for most modern developers, including C#, Java and Node.js.
- Platforms - Choose from lots of data platforms to integrate with including SQL, MongoDB and Cassandra.

Warning - Costs can run up quickly. As Cosmos DB scales, so does its price.

## Azure SQL
Managed Service - Microsoft with take care of hardware and infrastructure level needs

Migrate On-Prem Microsoft SQL server to Azure SQL seamlessly with a frictionless process. It can also save you money as you have a lower cost of ownership.

Built-in Machine Learning
1. Optimization - Suggestions on how to optimize and improve performance on Azure SQL instances
2. Warnings - You will get warnings of degrading instances, and if anything out of the ordinary is happening.

Cloud Benefits
- Scalability - Scale your Azure SQL instances and get high availability as well
- Space - Manage huge databases up to 100 TB in size, and can restore huge databases in a manner of minutes
- Security - Benefits from built-in security features of the Azure cloud platform

SQL Databases vs SQL Managed Instance

No Differences
Language features, database features, security features, data models

Differences

| Azure SQL Database                      | Azure SQL Managed Instance                           |
| --------------------------------------- | ---------------------------------------------------- |
| Most like the traditional SQL Server    | Aimed at migrating from on-premises                  |
| Recovery from automated backups only    | Recovery from automated backups and full SQL backups |
| Geo-replications                        | No geo-replications                                  |
| Autoscale supported in serverless model | No autoscale                                         |
| Automatic Tuning                        | No automatic tuning                                  |
| No SQL Server Profiler                  | SQL Server Profiler                                  |
| No SQL Server Agent                     | SQL Server Agent                                     |

## Azure Database for MySQL
Features
1. Open Source - MySQL is an open source project where any member of the community can contribute
2. Relational Database - Data in the database is connected through relations in the data itself.
3. Mature and Stable - Millions of applications and websites use MySQL. It is both a mature product and very stable

Advantages
- PaaS - The services infrastructure is managed by Microsoft
- Development Focus - Focus on developing your business strengths instead of managing servers and networks
- Choice of Language - Use the language and framework of your choice, such as PHP and WordPress
- High Availability - Cloud glitter can provide high availability and scalability with ease. MySQL can handle an increasing number of users.
- Azure Security Features - You get all the high standard Azure security features included.
- Cloud Capabilities - All the cloud PaaS features such as database patching, automatic backups and monitoring are included in the price.

Use Cases
- Web Apps
- E-Commerce 
- Mobile Apps
- Digital Marketing
- Finance Management
- Gaming

## Azure Database for PostgreSQL
About
1. Open-Source Database - it is an open-source relational database, similar to MySQL
2. The Name - It came "post" the database ingres, so the name became Postgres, which changed to PostgreSQL. 
3. Free and Stable - It is free and very stable. Constantly improved since 1996. Is used in millions of installations.

Features
- Extensions - Use a large number of extensions, such as JSONB, geospatial functions, indexing, integration with tools and much more. 
- Horizontal Scaling - Use very performant access to distributed data sets. In other words, use data faster across hundreds of servers.
- Performance Recommendations - Get recommendations based on usage on how to make your database perform better. Get notifications of distributed events.
- Fully Managed - Azure gives you automatic database patching, automatic backups and built-in monitoring. All included.

Use cases
- Financial Applications - Ideal for online transactions and integrates with mathematical software.
- Government - Governments use Postgres for geometric (GIS) data. One example is PostGIS, with is heavily used.
- Manufacturing - Downtime is disastrous, and PostgreSQL provides automated failover and full redundancy.

## Database Migration Services
About
1. Single Tool - One step migration for Microsoft SQL to Azure SQL
2. Documentation - Comprehensive step-by-step guides and documentation for helping you migrate.
3. Guides for non-MS - Very detailed guides for migrating from non-Microsoft databases.
