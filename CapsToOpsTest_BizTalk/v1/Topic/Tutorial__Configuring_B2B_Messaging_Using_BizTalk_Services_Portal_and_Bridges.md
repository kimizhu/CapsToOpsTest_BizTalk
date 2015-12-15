---
description: na
keywords: na
pagetitle: Tutorial: Configuring B2B Messaging Using BizTalk Services Portal and Bridges
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5084b53-55f2-41d9-9baf-b5f9c7df8548
---
# Tutorial: Configuring B2B Messaging Using BizTalk Services Portal and Bridges
[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] provides two key integration possibilities – enterprise application integration (EAI) and business-to-business (B2B) messaging using EDI. Using EAI, you can create [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)]s that are deployed on [!INCLUDE[azure_1](/Token/azure_1_md.md)]. Using B2B, you can create trading partners and agreements to process EDI messages on the cloud. You can then route the EDI messages to the already deployed [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)]s for additional processing. This tutorial provides step by step instructions to create, deploy, and test an end-to-end [!INCLUDE[af_integration](/Token/af_integration_md.md)] scenario.

## Business Scenario
Contoso and Northwind are two business partners. Contoso (the retailer) sends sales order messages to Northwind (the supplier). Northwind maintains all the sales order data in table called SalesOrder, which is housed in a SQL Server database within Northwind’s premises. Contoso can send either XML messages or EDI messages to Northwind. So Northwind has to implement a solution to enable the following:

- Contoso can send either an X12 message or an XML message for sales order.

- Contoso must send messages that conform to the schema for the sales order message expected by Northwind.

- Contoso can also send XML messages to directly insert sales order data in the SalesOrder table in Northwind’s SQL Server database.

To enable this scenario, Northwind does the following:

- For Contoso to send XML messages, Northwind configures an [!INCLUDE[request_response](/Token/request_response_md.md)] on [!INCLUDE[af_integration](/Token/af_integration_md.md)] to enable message validation and transformation. This bridge takes an input XML message, validates it against the sales order schema required by Northwind, and transforms the message to that schema. Northwind also uses [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] to enable connectivity to the on-premises SQL Server database from the [!INCLUDE[request_response](/Token/request_response_md.md)] deployed on the [!INCLUDE[sb2](/Token/sb2_md.md)].

- For Contoso to send EDI X12 messages, Northwind uses the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to configure and deploy an agreement in which Contoso can send an EDI/X12 message to Northwind.

The following illustration summarizes the scenario:

![](/Image/EAIEDITutorial_Scenario.gif)

## Integration Capabilities Demonstrated in this Tutorial
The scenario used for this tutorial helps us showcase the following integration capabilities of [!INCLUDE[af_integration](/Token/af_integration_md.md)]:

- **Message transportation**: The retailer and supplier can be present in different platforms and conform to different transport protocols and message formats. The [!INCLUDE[af_integration](/Token/af_integration_md.md)] implementation helps bridge these differences by understanding the different protocols and message formats.

- **Message validation**: While the incoming purchase order might be in different message formats for different retailers, the incoming purchase orders should conform to one of those defined message formats. This is achieved through message validation.

- **Message transformation**: The supplier adheres to a common purchase order format. Therefore, the incoming purchase orders have to be normalized to this common format. This is achieved through message transformation.

- **Hybrid connectivity**: The supplier's data store is an on-premises Microsoft SQL server. The normalized purchase order received through the cloud application has to be persisted in the on-premises data store. This is achieved through Hybrid connectivity.

## Before You Begin this Tutorial
To prepare a [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment, see [Administration and Development Task List in BizTalk Services](/Topic/Administration_and_Development_Task_List_in_BizTalk_Services.md). To set up the EDI message transfer, you need to access the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

## How to Use this Tutorial
This tutorial is written around a sample, **EAIEDITutorial.zip**, which is available to download at [MSDN Code Gallery](http://go.microsoft.com/fwlink/p/?LinkId=316856). You could use the sample and go through this tutorial to understand how the sample was built. Or, you could use this tutorial to create your own application. This tutorial is targeted towards the second approach so that you understand how this application is built. Also, as much as possible, the tutorial is consistent with the sample and uses the same names for artifacts (for example, schemas, transforms) as used in the sample.

## In This Section

- [Create and Deploy the BizTalk Services Project](/Topic/Create_and_Deploy_the_BizTalk_Services_Project.md)

- [Create and Deploy the Trading Partner Agreement](/Topic/Create_and_Deploy_the_Trading_Partner_Agreement.md)

## See Also
[Tutorials and Samples](/Topic/Tutorials_and_Samples.md)

