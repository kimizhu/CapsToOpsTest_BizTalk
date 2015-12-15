---
description: na
keywords: na
pagetitle: Add an Azure blob destination to receive invoice
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7dac2da4-1384-419c-986e-4a1bb61b9d0a
---
# Add an Azure blob destination to receive invoice
This topic provides instructions on how to add an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] project. After the **InvoiceBridge** processes the invoice message, it routes the message to an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob.

### To add an Azure blob

1. In the **ConnectedCar_Integration_Invoice** project, from the **Toolbox**, drag and drop the **Azure Blobs** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface.

2. Right-click the component, select **Properties**, and enter the following values:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Entity Name** <br /> <br />|Enter a unique and descriptive name of the Azure blob destination component. For this tutorial, enter this as **Invoice_Blob**. <br /> <br />|
   |**Shared Access Signature URL** <br /> <br />|Enter the shared access signature URL for the container in Azure Blob storage where the messages are routed to. <br /> <br />For instructions on how to generate the SAS, see [Create and Use a Shared Access Signature](http://msdn.microsoft.com/library/windowsazure/jj721951.aspx). You can also use the Azure Storage Explorer to generate SAS. For more information about the Azure Storage Explorer, see [Azure Storage Explorer](http://go.microsoft.com/fwlink/p/?LinkID=282292). <br /> <br />|

3. From the File menu, select **Save**.

## See Also
[Create a BizTalk Service project to process invoices](/Topic/Create_a_BizTalk_Service_project_to_process_invoices.md)

