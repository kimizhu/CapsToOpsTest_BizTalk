---
description: na
keywords: na
pagetitle: EDI, AS2, and EDIFACT Messaging (Business to Business)
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ceb9d0b1-3dfe-4979-b9c2-99a353ae98b5
---
# EDI, AS2, and EDIFACT Messaging (Business to Business)
In today’s world, to be successful as a business, enterprises must effectively manage data received from other organizations such as vendors and business partners. Data received from partner organizations is often categorized as business-to-business (B2B) data transfer. One of the standard and most commonly used protocols for B2B and EDI is X12. There are various solutions available that help you manage and process EDI data transfer.

[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] provides a [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] that enables you to manage your trading partners and B2B messaging. The [!INCLUDE[tpm_full](/Token/tpm_full_md.md)] enables service providers to add trading partners and configure agreements that can be deployed to [!INCLUDE[azure_1](/Token/azure_1_md.md)]. The trading partners can then be send X12 messages using HTTP, AS2, FTP/S, and SFTP as transports. Once the message is received, it will be processed by the B2B pipeline deployed on [!INCLUDE[azure_1](/Token/azure_1_md.md)] and is routed to the destination configured as part of the agreement.

Before you can use the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] for B2B messaging with your trading partners, you must register your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription with the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. See [Registering and Updating a BizTalk Service Deployment on the BizTalk Services Portal](/Topic/Registering_and_Updating_a_BizTalk_Service_Deployment_on_the_BizTalk_Services_Portal.md).

## In this Section

- [Building Blocks in B2B Messaging](/Topic/Building_Blocks_in_B2B_Messaging.md)

- [How do bridges resolve agreements at runtime?](/Topic/How_do_bridges_resolve_agreements_at_runtime_.md)

- [Configuring Agreements from a BizTalk perspective](/Topic/Configuring_Agreements_from_a_BizTalk_perspective.md)

- [Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

- [Trading Partner Management Object Model &#40;TPM OM&#41;: API Reference](/Topic/Trading_Partner_Management_Object_Model__TPM_OM):%20API%20Reference.md)

- [APPENDIX: Promoting Message Properties](/Topic/APPENDIX__Promoting_Message_Properties.md)

- [APPENDIX: Response Codes for X12 Bridges](/Topic/APPENDIX__Response_Codes_for_X12_Bridges.md)

## See Also
[BizTalk Services](/Topic/BizTalk_Services.md)

