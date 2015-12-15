---
description: na
keywords: na
pagetitle: Using the BizTalk Adapter Service (BAS)
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4263b70-bd4d-42b1-9d0b-619afdfaf8cd
---
# Using the BizTalk Adapter Service (BAS)
Using [!INCLUDE[lobconnect](/Token/lobconnect_md.md)], your cloud application can communicate with Line-of-Business (LOB) systems on-premises, in your network, behind your firewall. Using the LOB adapters in the [!INCLUDE[bap](/Token/bap_md.md)] (BAP), a [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] application can execute LOB operations to the following on-premises LOB systems:

- Microsoft SQL Server

- Oracle Database

- Oracle E-Business Suite

- SAP

- Siebel eBusiness Applications

Consider this scenario:

There is an on-premises SQL Server that stores Customer data, including Name, Shipping Address, Order History, and Payment Methods. You want to develop a purchasing application. When the order is being placed, this application retrieves the Name, Shipping Address, Order History, and Payment Methods from this SQL Server database. The goal is to host the application in the cloud and have it retrieve the customer data from this on-premises SQL Server.

[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] is your answer. You continue to maintain your on-premises SQL Server and allow the cloud to host your application. You can execute any LOB operation, like DELETE, INSERT, SELECT, UPDATE, from your cloud application.

[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] provides the following benefits:

- Cost effective: There are no individual relay endpoints in the cloud.

- Supports a mix of systems: You can connect a cloud application to an on-premises LOB system with the [!INCLUDE[bap](/Token/bap_md.md)].

- Maintenance: You continue to host your on-premises LOB system while the application is hosted in [!INCLUDE[azure_1](/Token/azure_1_md.md)].

- Flexibility: Execute a LOB operation in your table structure.

- Development: Use Visual Studio to create your cloud applications, just like creating BizTalk Server applications.

- Windows PowerShell: Use cmdlets to manage your LOB components (including creating, updating, and deleting).

## In This Section
[Development and Runtime Architecture: BizTalk Adapter Service](/Topic/Development_and_Runtime_Architecture__BizTalk_Adapter_Service.md)

[Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md)

[Connect to LOB systems from a BizTalk Services Project](/Topic/Connect_to_LOB_systems_from_a_BizTalk_Services_Project.md)

[PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md)

[LOB Security in BizTalk Adapter Service](/Topic/LOB_Security_in_BizTalk_Adapter_Service.md)

[Troubleshoot the BizTalk Adapter Service](/Topic/Troubleshoot_the_BizTalk_Adapter_Service.md)

## Reference

## Related Sections
