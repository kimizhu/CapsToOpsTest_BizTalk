---
description: na
keywords: na
pagetitle: Business Continuity and Disaster Recovery in BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2fe84ad4-24f0-4b42-bdf7-0cb283b587e2
---
# Business Continuity and Disaster Recovery in BizTalk Services
Describes business continuity and disaster recovery in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. It includes the possible issues and the capabilities provided.

For [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], Business Continuity issues belong to one of the following categories:

- Failure of individual servers, devices or network connectivity

- Corruption, unwanted modification or deletion of data

- Widespread loss of data center facilities

## Failure of individual servers, devices or network connectivity
For these types of failures, [Azure Business Continuity Technical Guidance](http://go.microsoft.com/fwlink/p/?LinkID=309061) provides some good information, including:

- Describes the Fabric Controller (FC); which monitors and manages role instances.

- Tips for developers when creating applications; including storing persistent data in an Azure Store Account or SQL Database.

- Tips for administrators, including using the Scale feature to handle increase or decrease demands.

To provide high availability, every [!INCLUDE[azure_2](/Token/azure_2_md.md)] BizTalk Service (except the Developer Edition) includes at least two role instances. Some Editions can also be scaled to add additional Units. See [BizTalk Services: Developer, Basic, Standard and Premium Editions Chart](http://go.microsoft.com/fwlink/p/?LinkID=302279) for more details.

An [!INCLUDE[azure_1](/Token/azure_1_md.md)] BizTalk Service uses [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)]. The [!INCLUDE[SQLAzDb](/Token/SQLAzDb_md.md)] has built-in features that provide fault tolerance, as described in [Business Continuity in Azure SQL Database](http://msdn.microsoft.com/library/windowsazure/hh852669.aspx).

## Corruption, unwanted modification or deletion of data
Data corruption, modifications, and deletions can occur for many reasons; including application errors, operator errors, and so on. [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] provides Backup and Restore functionality. It is recommended to create a backup of the BizTalk Service on a regular basis, including whenever a management operation (like updating the SSL certificate or modifying an EDI agreement) is made to the BizTalk Service. [BizTalk Services: Backup and Restore](http://go.microsoft.com/fwlink/p/?LinkID=329873) lists the backup and restore options for a BizTalk Service.

The Backup-Restore option doesn’t back up the BizTalk Services dependencies, including [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)]s, [!INCLUDE[azure_1](/Token/azure_1_md.md)] Storage, and [!INCLUDE[ac1](/Token/ac1_md.md)]. For these dependencies, consider the following:

- [Business Continuity in Azure SQL Database](http://msdn.microsoft.com/library/windowsazure/hh852669.aspx) provides information on [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)].

- [Azure Business Continuity Technical Guidance](http://go.microsoft.com/fwlink/p/?LinkID=309061) provides information on [!INCLUDE[azure_1](/Token/azure_1_md.md)] Storage. It is recommended to enable geo-replication on the Storage account.

- For [!INCLUDE[ac1](/Token/ac1_md.md)], you can create a new namespace. [Azure Business Continuity Technical Guidance](http://go.microsoft.com/fwlink/p/?LinkID=309061) provides information on [!INCLUDE[ac1](/Token/ac1_md.md)].

## Widespread loss of data center facilities
When you provision or create a backup of the BizTalk Service, you specify the datacenter. It is recommended to create backups to a different datacenter. If a datacenter disaster occurs, use the Restore functionality to restore an existing backup. [BizTalk Services: Backup and Restore](http://go.microsoft.com/fwlink/p/?LinkID=329873) lists the backup and restore options for a BizTalk Service.

The [Azure Service Dashboard](http://www.windowsazure.com/support/service-dashboard/) shows the status of the backend components of the BizTalk Service. Any issues with the backend components are communicated in this dashboard. This dashboard also lists the health state of any dependent components.

Backup the BizTalk Service often; daily is ideal.

## See Also
[BizTalk Services](/Topic/BizTalk_Services.md)
[BizTalk Services](/Topic/BizTalk_Services.md)
[Create the project in Visual Studio](/Topic/Create_the_project_in_Visual_Studio.md)

