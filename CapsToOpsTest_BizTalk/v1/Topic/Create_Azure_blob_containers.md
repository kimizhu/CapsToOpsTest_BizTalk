---
description: na
keywords: na
pagetitle: Create Azure blob containers
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e9a73545-cc1d-43fb-99b4-ca9ddd9394d3
---
# Create Azure blob containers
In this topic, we create [!INCLUDE[azure_2](/Token/azure_2_md.md)] Blob containers that are required for the solution. We create three containers, one to receive purchase order data before it is sent to the EDI send pipeline, one to receive purchase order data after it is processed by the EDI send pipeline, and one to receive invoice data from Fourth Coffee. We also generate the Shared Access Signature (SAS) URLs to access the blobs. The SAS URL is required for authentication while writing data to the blob.

### To create Azure blob containers

1. Create an [!INCLUDE[azure_2](/Token/azure_2_md.md)] storage account as described here: [Create an Azure Storage Account](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/#create-account). For this tutorial, name the storage account at **cloudcardemostore**.

2. Create a container called **purchaseorder** within the **cloudcardemostore** storage account. This container will store the purchaser order data received from customers. Create a container by performing the following steps:

   1. On the [!INCLUDE[azureportal1](/Token/azureportal1_md.md)], select **STORAGE**, and then select **cloudcardemostore**. In the **cloudcardemostore** dashboard, select **CONTAINERS**, and then from the command bar, select **ADD**.

   2. On the New Container dialog box, enter the name as **purchaseorder** and mark access as private.

   3. Select the check mark to create the container.

3. Repeat this step to create two more containers and name them **invoice** and **tosupplier**.

4. Create a Shared Access Signature (SAS) for all the containers. SAS is required for authentication while writing data into the container. For instructions on how to generate the SAS, see [Create and Use a Shared Access Signature](http://msdn.microsoft.com/library/windowsazure/jj721951.aspx). You can also use the Azure Storage Explorer to generate SAS. For more information about the Azure Storage Explorer, see [Azure Storage Explorer](http://go.microsoft.com/fwlink/p/?LinkID=282292).

## See Also
[Set up the integration layer](/Topic/Set_up_the_integration_layer.md)

