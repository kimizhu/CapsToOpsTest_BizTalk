---
description: na
keywords: na
pagetitle: Building Blocks in B2B Messaging
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 934e7251-ffb0-48cf-8294-92d59f82fb43
---
# Building Blocks in B2B Messaging
The key constituents of B2B messaging are the trading partners, business profiles, agreements, and bridges. This article provides information on each of these and how they are implemented in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. It also provides information about the flow of a typical B2B solution and how the different building blocks work together.

- [Trading partners](/Topic/Building_Blocks_in_B2B_Messaging.md#BKMK_Partners)

- [Business profiles](/Topic/Building_Blocks_in_B2B_Messaging.md#BKMK_Profiles)

- [Trading partner agreement](/Topic/Building_Blocks_in_B2B_Messaging.md#BKMK_Agreement)

- [Bridges](/Topic/Building_Blocks_in_B2B_Messaging.md#BKMK_Bridges)

- [Putting the blocks together](/Topic/Building_Blocks_in_B2B_Messaging.md#BKMK_Together)

## <a name="BKMK_Partners"></a>Trading partners
Each participating organization in a business relationship is a trading partner. A business partnership involves two or more trading partners. You can use the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to create a trading partner.

## <a name="BKMK_Profiles"></a>Business profiles
A trading partner’s business profile represents the business divisions inside a trading partner organization. For example, two business divisions, “Payment” and “Shipping”, within a trading partner organization can be represented as business profiles in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. Profiles include the property settings that are commonly used when configuring agreements between partners, such as the certificates that are used sign and encrypt messages exchanged between the partners.

### Certificates uploaded for a profile
Certificates uploaded to a partner’s profile are used to sign/un-sign and encrypt/decrypt messages.

## <a name="BKMK_Agreement"></a>Trading partner agreement
A Trading partner agreement is defined as a definitive and binding agreement between two trading partners for transacting messages over a specific B2B protocol. An agreement defines the protocol, and the related properties, that are used by the trading partners for exchanging messages.

## <a name="BKMK_Bridges"></a>Bridges
A bridge configuration defines the schema of the message to be processed, any transforms that must be used while processing the message, and the endpoints where the message is routed to. Bridges use agreements at runtime. For more information on how a bridge resolves to an agreement, see [How do bridges resolve agreements at runtime?](/Topic/How_do_bridges_resolve_agreements_at_runtime_.md)

## <a name="BKMK_Together"></a>Putting the blocks together
This section details the flow of a typical B2B solution and how the different building blocks work together. This section also lists some best practices for modeling a B2B solution.

1. Create partners representing all the organizations involved in a business trade. For example, if there are two business organizations involved in a business trade, you must create a trading partner for each of them. For instructions on how to create trading partners, see [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md).

2. Creating a partner automatically creates a default profile for the partner. For each business division within a partner organization, create more profile if required. Also, you must create the business profiles not just for the partner representing your organization but also for the partner with which you trade. For more information on creating profiles, see [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md).

3. Create agreements between the business profiles. For instructions on how to create agreements, see [Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md).

4. Create bridges to process the messages exchanged between the trading partners. See [Create an EDI bridge using BizTalk Services Portal](/Topic/Create_an_EDI_bridge_using_BizTalk_Services_Portal.md) or [Create an AS2 bridge using BizTalk Services Portal](/Topic/Create_an_AS2_bridge_using_BizTalk_Services_Portal.md).

## See Also
[EDI, AS2, and EDIFACT Messaging &#40;Business to Business&#41;](/Topic/EDI,_AS2,_and_EDIFACT_Messaging__Business_to_Business).md)

