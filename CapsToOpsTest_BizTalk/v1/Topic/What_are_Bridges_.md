---
description: na
keywords: na
pagetitle: What are Bridges?
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1aef098a-aec9-4258-adb0-ad5abfa5b820
---
# What are Bridges?
Bridges are entities that help in message mediation. Message mediation involves performing a series of processing steps such as decoding, validating, enriching, and transforming the message as it travels from its originating source to its destination. If we consider the ESB pattern where systems are loosely coupled and are communicating via messages, bridges can be thought of as a combination of an on-ramp, a pipeline, and an off-ramp. Following are the characteristics of bridges provided with [!INCLUDE[af_integration](/Token/af_integration_md.md)]:

- Bridges are composed of stages and activities where each stage is a message processing unit in itself.

- Each stage of a [!INCLUDE[bridge](/Token/bridge_md.md)] is atomic, which means either a message completes a stage or not. A stage can be turned *on* or *off*, indicating whether to process a message or simply let it pass through.

The following diagram presents a pictorial representation of how different stages of a pipeline are tied together:

![](/Image/AFINT_Bridges.gif)

## Templates for Bridges
There are two types of [!INCLUDE[bridge](/Token/bridge_md.md)] templates –*generic* and *specific*. A **generic** template is a customizable template and is the starting point of specific templates. You can use this template to create a customized bridge that suits your requirements. A **specific** template is a specialized case of the generic template, which is designed for a specific use. One example of a specific template is the **XML bridge** template that specializes in processing XML messages. This release of [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides only the specific bridge templates – [!INCLUDE[one-way](/Token/one-way_md.md)], [!INCLUDE[request_response](/Token/request_response_md.md)], and [!INCLUDE[passthru](/Token/passthru_md.md)]. This section provides more information about these bridges, including the stages, uses of the template, and so on.

## In This Section

- [Uses and Stages of Bridges](/Topic/Uses_and_Stages_of_Bridges.md)

- [Message Exchange Patterns for Bridges](/Topic/Message_Exchange_Patterns_for_Bridges.md)

- [Transports and Message Formats Supported for a Bridge](/Topic/Transports_and_Message_Formats_Supported_for_a_Bridge.md)

- [How Messages get Routed from a Bridge](/Topic/How_Messages_get_Routed_from_a_Bridge.md)

- [Route and Reply Actions: Bridging Protocol Mismatch](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md)

## See Also
[Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md)

