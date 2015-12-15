---
description: na
keywords: na
pagetitle: Set up the integration layer
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 05b90694-f49c-42e4-8bf4-c4d2f65434c3
---
# Set up the integration layer
The topics in this section demonstrate how to set up the core of the application, which is the integration layer. For this tutorial, let us assume that Contoso, Ltd. uses [!INCLUDE[af_integration](/Token/af_integration_md.md)] and other [!INCLUDE[azure_2](/Token/azure_2_md.md)] technologies to set up the integration layer and automate business transactions with its partners, such as Fourth Coffee. In this section, we perform the following steps to set up all the components of the integration layer:

- Create an [!INCLUDE[azure_2](/Token/azure_2_md.md)] storage account. Add three containers to that storage account, one each for:

   - Storing the purchase order message, which must be sent to Fourth Coffee before it is processed by the EDI send pipeline.

   - Storing the purchase order, which must be sent to Fourth Coffee after it is processed by the EDI send pipeline.

   - Storing the invoice received from Fourth Coffee.

- Create a Visual Studio solution with two [!INCLUDE[af_integration](/Token/af_integration_md.md)] projects. One [!INCLUDE[af_integration](/Token/af_integration_md.md)] project receives the messages from the customer, transforms it to a purchase order (X12 850) EDI message processes it, and then routes it to an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob. This application also inserts the purchase order data into a SQL Server database table.

   The other [!INCLUDE[af_integration](/Token/af_integration_md.md)] project receives the X12 810 invoice message from Fourth Coffee, transforms it to a format expected by the Connected Car application, and then routes it to another [!INCLUDE[azure_2](/Token/azure_2_md.md)] Blob. This application inserts the invoice data into a SQL Server database table and also sends out an e-mail to the customer with the order status.

   > [!NOTE]
   > If you want to use the sample [!INCLUDE[af_integration](/Token/af_integration_md.md)] project instead, you can download it from the MSDN code gallery at [http://go.microsoft.com/fwlink/p/?LinkId=390148](http://go.microsoft.com/fwlink/p/?LinkId=390148).

- Using the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], create and deploy an EDI agreement between Contoso, Ltd. and Fourth Coffee. The send-side of the agreement receives X12 850 purchase order message and routes it to an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob. Fourth Coffee consumes the message from the blob.

   The receive-side of the agreement receives the X12 810 invoice (corresponding to the purchase order) from Fourth Coffee and routes it to the EAI bridge for processing invoice messages.

- Create an [!INCLUDE[azure_2](/Token/azure_2_md.md)] worker role that regularly polls the [!INCLUDE[azure_2](/Token/azure_2_md.md)] blobs. This is required so that the original purchase order message that was routed to blob can be sent to the EDI send pipeline that is deployed as part of a trading partner agreement between Contoso, Ltd. and Fourth Coffee.

   > [!NOTE]
   > If you want to use the sample project instead, you can download it from [http://go.microsoft.com/fwlink/p/?LinkId=390152](http://go.microsoft.com/fwlink/p/?LinkId=390152).

This section provides instructions on how to create these components that constitute the integration layer for the end-to-end scenario.

## Prerequisites

- Install the certificate that was used to provision [!INCLUDE[af_integration](/Token/af_integration_md.md)] using the [!INCLUDE[azureportal1](/Token/azureportal1_md.md)].

- Provision a [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. For instructions, see [How To: Create or Modify a Service Bus Service Namespace](http://msdn.microsoft.com/library/windowsazure/hh690931.aspx).

- Install [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK. For instructions, see [Installing Azure BizTalk Services SDK](http://msdn.microsoft.com/library/windowsazure/hh689760.aspx).

- Install the [!INCLUDE[azure_1](/Token/azure_1_md.md)] .NET SDK. You can download the SDK from [http://go.microsoft.com/fwlink/p/?LinkId=378265](http://go.microsoft.com/fwlink/p/?LinkId=378265).

- Set up a SendGrid account for sending e-mails from applications deployed on [!INCLUDE[azure_1](/Token/azure_1_md.md)]. In the [!INCLUDE[af_integration](/Token/af_integration_md.md)] application, we use SendGrid to send e-mail out to the customers. For instructions on how to setup and use SendGrid, see [http://go.microsoft.com/fwlink/p/?LinkId=389151](http://go.microsoft.com/fwlink/p/?LinkId=389151).

- Setup a SQL Server database and create the SQL Server artifacts required for this tutorial. You can download the SQL scripts that create these artifacts from the **\Scripts** location under the sample. The sample is available at [MSDN Code Gallery](http://go.microsoft.com/fwlink/p/?LinkId=324220).

## In This Section

- [Create Azure blob containers](/Topic/Create_Azure_blob_containers.md)

- [Create a BizTalk Services solution](/Topic/Create_a_BizTalk_Services_solution.md)

- [Create a trading partner agreement](/Topic/Create_a_trading_partner_agreement.md)

- [Create an Azure worker role to poll the Azure blob](/Topic/Create_an_Azure_worker_role_to_poll_the_Azure_blob.md)

## See Also
[Using BizTalk Services from a Windows 8 Application](/Topic/Using_BizTalk_Services_from_a_Windows_8_Application.md)

