---
description: na
keywords: na
pagetitle: Add Source, Destination, and Bridge Messaging Endpoints
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a920966f-2095-4579-9164-da742f7f3353
---
# Add Source, Destination, and Bridge Messaging Endpoints
In the [BizTalk Services](/Topic/BizTalk_Services.md) topic, we saw that one of the core requirements from [!INCLUDE[af_integration](/Token/af_integration_md.md)] is to bridge the message and transport protocol mismatch between two disparate systems. In cloud parlance, we should think of each system on the cloud as an endpoint on [!INCLUDE[azure_1](/Token/azure_1_md.md)]. Rich messaging endpoints enable message exchange between these disparate applications (which are either extensions of on-premises applications or representing an application running on the cloud). However, given that the two systems are disparate and probably follow different messaging format and protocols, it becomes imperative that [!INCLUDE[azure_1](/Token/azure_1_md.md)] provides rich processing capabilities between the two endpoints. The processing capabilities could include the following:

- The ability to connect systems following different transport protocols

- The ability to validate the message originating from the source endpoint against a standard schema

- The ability to transform the message as required by destination endpoints

- The ability to enrich the message by adding properties to the message context. The properties can then be used to route the message to a destination or an intermediary endpoint.

All these capabilities are made available through *rich messaging endpoints* available as part of [!INCLUDE[af_integration](/Token/af_integration_md.md)]. The following diagram depicts how rich messaging endpoints bridge mismatches between systems and applications.

![](/Image/AFINT_RichMsgEndPoint.gif)

To sum it up, [!INCLUDE[af_integration](/Token/af_integration_md.md)] offers four major components (connectivity, validation, enrichment, transformation) that can be stitched together to provide rich messaging endpoints.

- **Connectors**: These bridge the gap between different transport protocols as well as different LOB applications that exist on the premise behind a firewall but expose their operational endpoints on the cloud. Bridges accept incoming messages from different protocols such as HTTP, FTP, and SFTP. Bridges can send outgoing messages to different protocols such as HTTP, FTP, SFTP as well as other endpoints such as Azure Blobs, [!INCLUDE[sb2](/Token/sb2_md.md)] Queues, Topics, and Relays.

   In addition, [!INCLUDE[af_integration](/Token/af_integration_md.md)] also provides connectivity to on-premise LOB applications such as SQL Server, SAP, Siebel, and Oracle databases/E-Business Suite. For more information, see [Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md).

   While setting up connectivity, you can also set rules based on which the message is transferred to different endpoints. For more information, see [Routing Messages from Bridges to Destinations in the BizTalk Service Project](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md).

- **Validation, Enrichment, and Transformation**: [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides these capabilities as different stages of a ‘bridge’. For more information, see [What are Bridges?](/Topic/What_are_Bridges_.md).

## In This Section

- [What are Bridges?](/Topic/What_are_Bridges_.md)

- [Create Rich Messaging Endpoints on Azure](/Topic/Create_Rich_Messaging_Endpoints_on_Azure.md)

- [Tools for Creating Message Schemas](/Topic/Tools_for_Creating_Message_Schemas.md)

- [Flat-file Support In One-Way Bridge](/Topic/Flat-file_Support_In_One-Way_Bridge.md)

- [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md)

- [Tracking Messages Processed by the Bridge](/Topic/Tracking_Messages_Processed_by_the_Bridge.md)

## See Also
[BizTalk Services](/Topic/BizTalk_Services.md)

