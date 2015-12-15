---
description: na
keywords: na
pagetitle: Create Rich Messaging Endpoints on Azure
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18375cf4-5717-4384-aed9-c9d4098b87ec
---
# Create Rich Messaging Endpoints on Azure
The topic [Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md) discusses how such endpoints provide the ability to connect to disparate LOB applications and the ability to validate, transform, and extract properties from a message. The topic [Tools for Creating Message Schemas](/Topic/Tools_for_Creating_Message_Schemas.md) provides information on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface that can be used to configure such endpoints.

An end-to-end message processing entity may contain a message source (for receiving the message), message processing unit (such as a bridge), and finally a message destination (where the message is routed). So, configuring a rich messaging endpoint might include configuring all three components. This section provides the procedural information on how to configure all these components using the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

> [!NOTE]
> Even though **Transforms** are a part of rich messaging endpoints, they can either be configured as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] or created separately before they are added to the message flow.

## In This Section

- [Add a Message Source to the Bridge](/Topic/Add_a_Message_Source_to_the_Bridge.md)

- [Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md)

- [Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md)

- [Routing Messages from Bridges to Destinations in the BizTalk Service Project](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md)

- [Deploying and Refreshing the BizTalk Services Project](/Topic/Deploying_and_Refreshing_the_BizTalk_Services_Project.md)

## See Also
[Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md)

