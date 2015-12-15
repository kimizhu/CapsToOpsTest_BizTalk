---
description: na
keywords: na
pagetitle: How Messages get Routed from a Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c232b711-5654-4cea-af7a-7bba81c863e4
---
# How Messages get Routed from a Bridge
There can be many aspects to a simple routing operation between two components of a message flow. These could be:

- **Where to route the message to?** As part of this, you define the destination of the message that has been processed by the [!INCLUDE[bridge](/Token/bridge_md.md)]. See [The Routing Destination](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_Connect)

- **On what condition will the routing be done?** This typically is driven by the business scenario which describes the parameters on which the routing is done. For example, all requests for mobile phone divisions should be passed on to department A, and so on. See [The Routing Condition](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_Filter).

- **In which order should the routing be done?** If there is more than one condition for routing, you must also set the order in which the routing conditions are honored. See [The Routing Order](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_Order).

- **Do any specific actions need to be performed on the message before routing?** This is especially targeted for protocol bridging scenarios where the message sender and the message receiver operate on different message protocols. To bridge such protocol mismatch, you can perform certain actions on the message before it is finally routed. For more information on how the protocol mismatch is bridged, see [Route and Reply Actions: Bridging Protocol Mismatch](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md).

All these points are discussed in detail, with instructions on how to achieve them, at [Routing Messages from Bridges to Destinations in the BizTalk Service Project](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md).

## See Also
[What are Bridges?](/Topic/What_are_Bridges_.md)

