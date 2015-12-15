---
description: na
keywords: na
pagetitle: Add an Azure blob destination to receive purchase order
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bd64934-75f7-4d73-ac60-cbfeb5ef9a6b
---
# Add an Azure blob destination to receive purchase order
This topic provides instructions on how to add an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] project. After the **PurchaseOrderBridge** processes the customer order message, it routes the message to a [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob.

### To add an Azure blob

1. In the **ConnectedCar_Integration_PurchaseOrder** project, from the **Toolbox**, drag and drop the **Azure Blobs** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface.

2. Right-click the component, select **Properties**, and enter the following values:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Entity Name** <br /> <br />|Enter a unique and descriptive name of the Azure blob destination component. For this tutorial, enter this as **PO_Blob**. <br /> <br />|
   |**Shared Access Signature URL** <br /> <br />|Enter the shared access signature URL for the container in Azure Blob storage where the messages are routed to. <br /> <br />For instructions on how to generate the SAS, see [Create and Use a Shared Access Signature](http://msdn.microsoft.com/library/windowsazure/jj721951.aspx). You can also use the Azure Storage Explorer to generate SAS. For more information about the Azure Storage Explorer, see [Azure Storage Explorer](http://go.microsoft.com/fwlink/p/?LinkID=282292). <br /> <br />|

3. From the File menu, select **Save**.

## See Also
[Create a BizTalk Service project to process purchase orders](/Topic/Create_a_BizTalk_Service_project_to_process_purchase_orders.md)

