---
description: na
keywords: na
pagetitle: Message Exchange Patterns for Bridges
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 300b4e72-27f3-4526-a3cd-44f00a8b7a53
---
# Message Exchange Patterns for Bridges
Bridges being message intermediaries between the clients and services, they must support the different message exchange patterns agreed upon between the respective clients and services. Currently, the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] supports two message exchange patterns – [!INCLUDE[one-way](/Token/one-way_md.md)] and [!INCLUDE[request_response](/Token/request_response_md.md)]. [!INCLUDE[passthru](/Token/passthru_md.md)] also supports only one-way message exchange pattern. Note that the message exchange patterns are considered at the application level, which means, that for a [!INCLUDE[request_response](/Token/request_response_md.md)], the client sending a message to the service expects a response back. For [!INCLUDE[one-way](/Token/one-way_md.md)], no such response is expected.

In an [!INCLUDE[one-way](/Token/one-way_md.md)], the client sends a message to the service but does not expect or request a response back. An [!INCLUDE[one-way](/Token/one-way_md.md)] contains the following stages:

- Validate

- Enrich, pre-transform

- Transform

- Enrich, post-transform

See [Uses and Stages of Bridges](/Topic/Uses_and_Stages_of_Bridges.md).

### <a name="BKMK_ConstOneWay"></a>Constraints on Using an XML One-Way Bridge
An [!INCLUDE[one-way](/Token/one-way_md.md)] can route messages to any destination that can be added to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. The only consideration is that when you route a message from a [!INCLUDE[one-way](/Token/one-way_md.md)] to two-way destination endpoints, such as Two-Way Relay Endpoint, Two-Way External Service Endpoint, or an [!INCLUDE[request_response](/Token/request_response_md.md)], then the response message that is received from any of these two-way endpoints is ignored by the [!INCLUDE[one-way](/Token/one-way_md.md)].

In an [!INCLUDE[request_response](/Token/request_response_md.md)], the client sends a message to the service and expects a response back.

### Request Path
The request path of the bridge contains the following stages:

- Validate

- Enrich, pre-transform

- Transform

- Enrich, post-transform

### Reply Path
The response path of the bridge contains the following stages:

- Enrich, pre-transform

- Transform

- Enrich, post-transform

- Reply Action

For more information about each of these stages, see [Uses and Stages of Bridges](/Topic/Uses_and_Stages_of_Bridges.md). For more information about Reply Action, see [Route and Reply Actions: Bridging Protocol Mismatch](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md).

### <a name="BKMK_ConstTwoWay"></a>Constraints on Using an XML Request-Reply Bridge
You can use an [!INCLUDE[request_response](/Token/request_response_md.md)] only for routing messages to two-way relay endpoints, two-way external service endpoints, or other [!INCLUDE[request_response](/Token/request_response_md.md)].

In a [!INCLUDE[passthru](/Token/passthru_md.md)], the client sends a message of any message type to the bridge and does not expect a response back. A [!INCLUDE[passthru](/Token/passthru_md.md)] contains only an Enrich stage and is only a one-way bridge.

### <a name="BKMK_ConstPassThru"></a>Constraints on Using a Pass-Through Bridge
The constraints for a [!INCLUDE[passthru](/Token/passthru_md.md)] are same as the constraints for an [!INCLUDE[one-way](/Token/one-way_md.md)]. For more information, see [Constraints on Using an XML One-Way Bridge](/Topic/Message_Exchange_Patterns_for_Bridges.md#BKMK_ConstOneWay).

## See Also
[What are Bridges?](/Topic/What_are_Bridges_.md)

