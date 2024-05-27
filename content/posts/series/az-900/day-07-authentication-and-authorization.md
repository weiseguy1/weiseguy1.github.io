---
title: "AZ-900 Day 07: Authentication and Authorization"
date: 2024-05-09T18:45:18-05:00
description: ""
draft: true
type: "post"
tags: ["az-900", "azure", "devops", "series"]
showTableOfContents: true
---

![Cover Art](/images/posts/series/az-900/day-07/cover.png)

## Identity Services

| Authentication          | Authorization              |
| ----------------------- | -------------------------- |
| Making sure you are you | comes after authentication |
| Confirm identity        | Do you get access?         |
| First test for access   | Granular control           |

### Access Management
1. Authentication vs Authorization - You must know the difference to create effective access management
2. Keep out the baddies - Access management is critical to ensure only the right people and processes have access

## Azure Active Directory

### Active Directory
1. Traditional Office Use - Active Directory was designed for traditional office use with computers and printers
2. What is "Web"? - The web as a concept or service was not part of the design of Active Directory. Web services were not part of the original vision of Active Directory in 2000
3. Authentication - Active Directory authentication uses services that aren't available on Azure

**Disclaimer: Active Directory IS NOT Azure Active Directory**

### Azure Active Directory (AAD) Service
1. Mandatory - You can't have an Azure account without an AAD service.
2. First User - Every Azure account needs a first user and this user is in the initial AAD instance.
### Tenant 
1. Organization - A tenant represents the organization
2. Dedicated AAD - A tenant is a dedicated instance of AAD that an organization receives when signing up for Azure.
3. Separate - Each tenant is distinct and completely separate from other AAD tenants
4. One User = One Tenant - Each user in Azure can only belong to a single tenant. Users can be guests of other tenants though
### Subscriptions
1. Billing Entity - All resources within a subscription are billed together
2. Cost Separation - You can have multiple subscriptions within a tenant to separate costs
3. Payment - If a subscription isn't paid, all the resources and services associated with the subscription stop.

### Hybrid Cloud Architecture
- AAD can help manage on-prem and Azure accounts


### Azure AD now Part of Microsoft Entra
- Microsoft Entra = New Product Family
- Includes all of Microsoft's identity and access capabililties
- Exam Perspective: Know that Azure AD is part of the broader Microsoft Entra product family
	- Azure Active Directory
	- Permissions Management
	- Verified ID

## Zero Trust Concepts

### Classic Trusted vs Untrusted Model
- Trusted Perimeter
- Trust Boundary for secure access
	- Example: Corporate network
	- Restrict private access to secure networks

### Challenges with Trusted Perimeter Model
- Must be on corporate network to access resources
	- Remote work is a challenge
		- VPN is extension of trusted perimeter
	- Mobile device access even more challenging
- Rogue user/malware inside trusted perimeter network can cause havoc
	- Broad scope of access

### What is Zero Trust?
- All users assumed untrustworthy unless proven otherwise
	- Trusted by identity
	- Regardless of location (trusted/untrusted networks)
	- Least privilege access - just enough permissions to perform job
	- Simplified, centralized management
- Zero Trust = Trusted identities, not locations

### Zero Trust in Action
- Access Microsoft 365 email, documents, and resources for remote workforce
	- Access from anywhere
	- Authenticate with identity, not over VPN
- Centrally control access with Conditional Access policies
- Allow access only from approved managed devices
	- Independent from network location

## Multi-Factor Authentication

### Approach
- Something you know
- Something you have
- Something you are


## Conditional Access

### Conditional Access Concepts
- Authentication Protections beyond Username/Password
- If/then policies to grant access
	- if (user) meets these conditions (signals), then grant/block access to defined applications
- Often paired with multi-factor authentication (MFA)
	- Centrally applied MFA enforcement
	- Does not rely on end user enabled MFA
### How it works
- Create Conditional Access Policy
	- Assign signals (conditional)
	- Users/groups
	- Applications to grant/deny access
	- Location (IP)
	- Approved devices
- Access decisions (grant/block access)

### Conditional Access Scenarios
- Enforce MFA for all administrators/all users
- Block sign-ins using legacy authentication protocols
- Grant access only to specific locations
- Require organization-managed devices for application sign-in

## Passwordless Authentication

### Security vs. Convenience: The Never-Ending Conflict
- Multi-Factor Authentication is more secure but less convenient
	- More steps to login
		- Password and device/biometrics
		- Increased user frustration:
			- If everything is not working as expected
			- Overall, less convenient
- Objective: Increase Convenience while staying secure
	- Remove password from system login
	- Replace with:
		- Something you have: (Phone/key fob)
		- Something you know/are (Fingerprint/face unlock/PIN)

### Passwordless Authentication Methods
- Microsoft Authenticator App
	- Microsoft's MFA mobile app
		- Configure in Azure AD
	- Authenticate in app with biometrics/PIN
- Windows Hello
	- Face recognition in Windows
- FIDO2 Security Key
	- Hardware key

## External Guest Access

### How to collaborate with external users?
- Scenario: Working with outside consultant to streamline Azure or Azure AD configuration
	- Create separate organization account for external user.
		- Requires external user to juggle two accounts
	- Invite guest user to Azure tenant
		- Guest user uses existing account as an external collaborator
		- Business-to-Business (B2B) collaboration

### Adding a Guest User
- Invite a variety of account types (identity providers)
	- Microsoft, Google, Facebook
	- Other external identity providers
- Assign permissions for guest account
	- Principle of least privilege 
	- Different permissions between Azure AD and Azure subscription
- Optional: Assign guest user to application
- Optional: Apply cross-tenant Conditional Access Policy
	- Require MFA
	- Require approved managed devices

### Scenario: Inviting an External Consultant
- Configure identity provider (if non-Microsoft)
- Invite external party
- After guest user accepts invitation, assign permissions
	- Optionally: Assign apps, apply Conditional Access policy

## Azure Active Directory Domain Services

### Limitations of Azure AD and Cloud Migration
- Legacy Applications
	- Unable to user modern authentication protocols (OAuth 2.0)
- Require traditional Active Directory (AD DS) management/protocols
	- Group Policy
	- LDAP
	- NTLM
	- Kerberos

### Possible Solutions?
- Continue using on-prem AD
	- Sync to Azure AD with Azure AD Connect
- Configure AD server on Azure VM
	- Also known as self-managed AD DS
	- You maintain/configure the operating system
- Azure Active Directory Domain Services (Azure AD DS)
	- Managed Active Directory Domain Services
	- Provides classic AD features in a managed service
		- Group Policy, LDAP, Kerberos, domain join

### How Azure AD DS Works
- Azure AD DS is a managed service
	- No need for OS configuration/management
	- Behind the scenes: two Windows domain controllers for high availability
- Create unique namespace/domain name
	- Example: aadds-companyname.com
	- Standalone domain, not extension of on-premises AD domain
- One-way sync from Azure AD to Azure AD DS
	- Syncs users, groups and credentials
	- Azure AD may also bidirectional sync with on-prem AD

### Scenario: Azure AD DS
- Lift and shift legacy enterprise applications to Azure VMs
	- Application does not support modern authentication
- Requirement to integrate application with classic cloud-hosted AD using managed services
- Cloud-hosted legacy application authenticates with Azure AD DS

## Single Sign-On

### Azure SSO
- Azure Active Directory Seamless Single Sign-On
	- Enabled SSO on AAD
	- Seamlessly use all applications without logging in
	- Single username and password
