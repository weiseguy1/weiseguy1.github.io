---
title: "AZ-900 Day 06: Storage"
date: 2024-04-21T15:12:58-05:00
description: ""
draft: true
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/azure-series-day-06-storage.png)

## Introduction 
Storage Account = Unique Azure Namespace
- Every object in Azure has its own web address
- Example
	- acloudguru.`<storage-type>`.core.windows.net

## Section 6.1: Blob Storage 
Blob means "Binary Large Object"
(which is pretty much anything)

### Storage Levels
- Storage Account
- Container
- Blob

### Scenarios
- Images - Store various sizes and formats as a single image storage
- All Types - Store any kind of files and have distributed access through the Azure cloud storage
- Streaming - Stream audio and video directly from your blob storage
- Log Files - Write to log files regardless of size a frequency
- Data Store - Store any kind of data at scale, such as for archiving, backup, restore and disaster recovery

### Blob Types 
1. Block - Store text and binary data up to 4.7TB. Made up of individually managed blocks of data
2. Append - Block blobs that are optimized for append operations. Works well for logging where data is constantly appended
3. Page - Store files up to 8TB. Any part of the file could be accessed at any time, for example a virtual hard drive

### Pricing Tiers
- Hot - Frequently accessed files. Lower access times and higher access costs.
- Cool - Lower storage costs and higher access times. Data remains here for at least 30 days.
- Archive - Lowest costs and highest access times.

## Section 6.2: Disk

### Managed Disk
- Azure Manages - You don't have to worry about backup and uptime
- Size and Performance - Microsoft and Azure guarantees size and performance as per your agreement with them
- Upgrade - Easy to upgrade your disk size and type

### Disk Types
- HDD - Spinning hard drive. Low cost and suitable for backups
- Standard SSD - Standard for production. Higher reliability, scalability and lower latency over HDD
- Premium SSD - Super fast and high performance. Very low latency. Use for critical workloads
- Ultra Disk - For the most demanding, data-intensive workloads. Disks are up to 64TB.

## Section 6.3: File

### On-Premises
Company -> On-Premises Storage 
Issues
1. Constraints - You only have a limited amount of storage
2. Backups - TIme and resources spent on maintaining backups
3. Security - It can be hard to keep all data secure at all times. Specialist assistance often needed. 
4. File Sharing - Can be difficult to share files across teams and organizations

Benefits
1. Sharing - Share access to the Azure file storage across machines and provide access to your on-premises infrastructure
2. Managed - You don't have to worry about hardware or operating systems.
3. Resilient - Network and power outages won't affect your storage

### Scenarios
- Hybrid - Supplement or replace your existing on-premises file storage solution
- Lift and Shift - Move your existing file storage and related services to Azure

## Section 6.4: Archive
### Overview
- Requirements - Policies, legislation and recovery can be requirements for archiving data. These can be very large amounts of data.
- Lowest Price - The archive tier is the lowest price for storage on Azure. A few dollars a month can get you terabytes of space. 
- Features - Durable, encrypted and stable. Perfectly suited for data that is accessed infrequently
- Free Up Premium Storage - With cheap archive storage you can free up your more premium on-premises storage.
- Secure - Fully secure to allow for any personal data such as financial records, medical data and more.
- Blob - Archive storage is blob storage, so the same tools will work for both

## Section 6.5: Storage Redundancy 

Data redundancy protects against unplanned failures

Redundancy - Multiple, Replicated Copies of Data
If one copy fails/is inaccessible, data is still available.

Azure Storage always creates multiple copies for your data:
- Automatic 
- Minimum of three copies
- Invisible to end user

Multiple Redundancy Options 
- Different location scopes
	- Single zone, multiple zones, multiple regions
- Higher availability -> higher cost

| Name                              | Region type | Description                                                                                                               |
| --------------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------ |
| Locally-redundant storage (LRS)   | Single |  Lowest-cost option with basic protection against server rack and drive failures. Recommended for non-critical scenarios   |
| Geo-redundant storage (GRS)       | Multi |  Intermediate option with failover capabilities in a secondary region. Recommended for backup scenarios                    |
| Zone-redundant storage (ZRS)      | Single | Intermediate option with protection against datacenter-level failures. Recommended for high availability scenarios        |
| Geo-zone-redundant storage (GZRS) | Multi | Optional data protection solution that includes the offering of both GRS and ZRS. Recommended for critical data scenarios |
All options include: 
- Three copies in primary region
- Three copies in the secondary region (multi-region options)

### LRS
Three copies in a single location (datacenter/zone)
1. Lowest-cost option
2. Protect against single disk failure
3. Does not protect against zone or regional outage

### ZRS
Three copies across three availability zones
1. One copy in each zone
2. Protect against zone outage but not regional outage

### GRS
Three copies in two regions
1. Three copies in primary regional physical location (LRS)
2. Three copies in secondary (paired) region physical location (LRS)
3. Protect against primary region failure but no primary region zone redundancy
4. Can configure read access from secondary region for high availability

### GZRS
Maximum redundancy
1. Copy across three availability zones in primary region (ZRS)
2. Three copies in secondary region physical location/zone (LRS)
3. Protect against primary region failure and primary region zone failure
4. Can also configure read access from secondary region for high availability

## Section 6.6: Moving Data
Concept: Moving Data into and out of Azure Storage
Different solution based on:
- Transfer frequency (occasional/continuous)
- Data size
- Network bandwidth

**AZ-900 focus for smaller, occasional transfers:**
- AzCopy
- Azure Storage Explorer
- Azure File Sync


### AzCopy
CLI utility
1. Transfer blobs and Azure Files
2. Useful for scripting data transfers

```
azcopy cp "funny-llamas.mp4" "https://mystorageaccount.blob.core.windows.net/my-container"
```

### Storage Explorer
GUI interaction
1. Downloaded application
2. User-friendly graphical interface 
	- Drag-and-drop interactions
3. Move all storage account formats

### Azure File Sync
Synchronize Azure Files with On-Prem File Servers
Local file server performance + cloud availability
Use cases:
- Backup local file server
- Synchronize files between multiple on-prem locations
- Remote users access Azure Files
- Transition to only Azure Files for file server

## Section 6.7: Additional Migration Options

### Azure Data Box
Scenario: Transfer LOTS of data and/or limited bandwidth
- Lots = Too much to transfer over the internet
- Relative to available network bandwidth
- Offline data transfer to/from Azure
- Copy data to physical data storage device (Data Box)
	- Encrypted 
	- Rugged
- Ship Data Box to/from Azure
	- **To Azure**: Data Box data transferred to storage account
	- **From Azure**: Data Box delivered to on-prem location for on-site transfer

### Data Box Use Cases
- Initial bulk data migration
- Disaster Recovery
	- Restore Azure backup to on-premises location
- Security requirements
	- Sensitive data that cannot be sent over the internet

### Azure Migrate
Migrate non-Azure resources into Azure
- Servers
- Databases
- Applications

Includes, but not limited to, migration to storage acccounts

### Azure Migrate Scenario: Migrate Datacenter to Azure
- Discover dependent resources to migrate
- Migrate VMs
- Migrate databases to managed database services (e.g., Azure SQL).
- Migrate on-prem applications and dependencies
- Migrate bulk data with Data Box

## Section 6.8: Premium Performance Options
Premium Performance Options for Low-Latency Requirements
- Stored on SSDs
- Key considerations:
	- Available storage types for each performance option
	- Redundancy options
		- Trade more performance for less redundancy
		- LRS/ZRS only for all types
	- All premium options have a higher cost

### Storage Account Performance Options
Standard 
- Standard general-purpose v2
	- The default - supports all storage types
	- All redundancy options
Premium
- Premium block blobs
- Premium page blobs
- Premium file share

### Premium Block Blobs
Supported Storage Types
- Blob Storage 
- Ideal for low-latency blob storage workloads
	- AI applications, IoT analytics

### Premium Page Blobs
Supported Storage Types
- Page blobs
	- Unmanaged virtual disk (currently being retired)
	- Standalone API access

### Premium File Share
Supported Storage Types
- Azure Files
	- Ideal for high-performance enterprise (file server) applications
	- Supports both Server Message Block (SMB) and Network File System (NFS) file shares
		- Windows/Linux file shares

