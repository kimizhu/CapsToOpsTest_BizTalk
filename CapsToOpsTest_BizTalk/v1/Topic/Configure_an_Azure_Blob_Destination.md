---
description: na
keywords: na
pagetitle: Configure an Azure Blob Destination
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8452ce71-c425-4de1-87d4-35a8bfe1bf88
---
# Configure an Azure Blob Destination
Configure an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob destination for sending messages from a [!INCLUDE[bridge](/Token/bridge_md.md)] to a blob storage on [!INCLUDE[azure_2](/Token/azure_2_md.md)]. You can use an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob as a destination component only with [!INCLUDE[one-way](/Token/one-way_md.md)]. See [Create an XML One-Way Bridge](/Topic/Create_an_XML_One-Way_Bridge.md) to learn how to configure the bridge. Once you have added an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob destination component to the [!INCLUDE[msgflow](/Token/msgflow_md.md)] surface, select **Connector** from the **Toolbox** and connect the [!INCLUDE[bridge](/Token/bridge_md.md)] to the Azure blob component.

### To add an Azure blob destination to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. See the steps at [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area thenselect **Properties**. Enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)]URL into the **BizTalk Service URL** property.

3. From the **Toolbox**, drag and drop the **[!INCLUDE[azure_2](/Token/azure_2_md.md)] Blob Destination** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface.

4. Right-click the component and select **Properties**. The following table provides information about the properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Entity Name** <br /> <br />|Enter a unique and descriptive name of the Azure blob destination component. <br /> <br />|
   |**Shared Access Signature URL** <br /> <br />|Enter the shared access signature (SAS) URL for the container in Azure Blob storage where the messages are routed to. Note that the SAS URL must include the ‘si’ parameter. The ‘si’ parameter is included in the SAS URL if it was created using a shared access policy. <br /> <br />For instructions on how to generate the SAS URL, see [Create and Use a Shared Access Signature](http://msdn.microsoft.com/library/windowsazure/jj721951.aspx). You can also use the Azure Storage Explorer to generate the SAS URL. For more information about the Azure Storage Explorer, see [Azure Storage Explorer](http://go.microsoft.com/fwlink/?LinkID=282292). <br /> <br />|

5. From the File menu, click **Save**.

## See Also
[Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md)

