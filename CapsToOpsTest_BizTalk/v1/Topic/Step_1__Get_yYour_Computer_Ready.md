---
description: na
keywords: na
pagetitle: Step 1: Get yYour Computer Ready
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.service: multiple
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc167337-3da2-4724-ad59-0867db354ffd
---
# Step 1: Get yYour Computer Ready
This topic provides you with instruction and pointers to set up your computer on which you will perform the steps to set up the hybrid integration scenario described in [Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server](/Topic/Tutorial__Using_Azure_BizTalk_Services_to_Integrate_with_an_On-Premises_SAP_Server.md). You must do the following to set up your computer:

- Install **[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK** at [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057). You use this SDK to configure and deploy the [!INCLUDE[one-way](/Token/one-way_md.md)] that sits between the EDI agreement and the relay endpoint.

- Install **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**. You use this to expose the **Send** operation on an IDOC as a relay endpoint on [!INCLUDE[sb2](/Token/sb2_md.md)].You can download the installer from [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057). Refer to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] installation guide at [http://go.microsoft.com/fwlink/p/?LinkId=237092](http://go.microsoft.com/fwlink/p/?LinkId=237092) to install the software prerequisites for [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK and [!INCLUDE[lobconnect](/Token/lobconnect_md.md)].

- Install the **WCF LOB Adapter SDK**. This is required for installing the [!INCLUDE[bap](/Token/bap_md.md)] on the computer.

- Install the **[!INCLUDE[bap](/Token/bap_md.md)]**. This contains the SAP adapter that is required to establish connectivity to an SAP Server and for exposing SAP artifacts as operations.

- Install the **SAP client libraries**. The SAP adapter needs these libraries to connect to an SAP Server. For information on where to install the SAP client libraries from, refer to the Adapter Pack installation guide (BizTalkAdapterPack_InstallationGuide.htm) at [http://go.microsoft.com/fwlink/p/?LinkId=240161](http://go.microsoft.com/fwlink/p/?LinkId=240161).

- Download and extract the **EDI message schemas** (MicrosoftEdiXSDTemplates.zip) available at [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057). This contains the X12 850 Purchase Order message schema that is required for the business scenario we use for this article.

After you have finished installing and downloading these components, you are ready to start setting up the business scenario.

## See Also
[Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server](/Topic/Tutorial__Using_Azure_BizTalk_Services_to_Integrate_with_an_On-Premises_SAP_Server.md)

