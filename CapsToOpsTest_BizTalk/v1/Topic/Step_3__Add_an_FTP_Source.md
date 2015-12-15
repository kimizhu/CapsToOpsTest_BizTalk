---
description: na
keywords: na
pagetitle: Step 3: Add an FTP Source
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb64ad06-3957-4023-a3ec-e9f7a9b35f82
---
# Step 3: Add an FTP Source
In this step, you add an FTP source to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. An FTP source represents the FTP Server where Fabrikam drops the flat-file message to be sent to Contoso.

### To add an FTP source

1. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] area, right-click anywhere on the design area, and select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

2. From the **Toolbox,** drag and drop an **FTP Source** component onto the design area.

3. Right-click the component and select **Properties**. The following table describes these properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Content Encoding** <br /> <br />|Specify the character encoding of the message. Default is **UTF8**. For this tutorial, retain the default. <br /> <br />|
   |**Content Type** <br /> <br />|Specify Text or XML as the message file type. Default is **Text**. For this tutorial, retain the default. <br /> <br />|
   |**Entity Name** <br /> <br />|Specify a unique and descriptive name of the FTP Source component. For this tutorial, specify **OrdersSource**. <br /> <br />|
   |**File Mask** <br /> <br />|Specify a File Mask to filter the messages pulled from the FTP server. For this tutorial, enter **&#42;.txt**. <br /> <br />|
   |**Folder Path** <br /> <br />|Specify the folder on the FTP server that contains the messages to retrieve.  For this tutorial, Contoso pulls all the messages from a **MessageToContoso** folder on the FTP server. Hence, enter **MessageToContoso**. <br /> <br />|
   |**FTP Transfer Mode** <br /> <br />|Specify **Binary** or **ASCII** as the mode of transfer. Default is **Binary**. For this tutorial, retain the default. <br /> <br />|
   |**Initial Status** <br /> <br />|Specify **Stop** or **Start** for the FTP Source. Default is **Start**. For this tutorial retain the default. If set to **Start**, the FTP Source component will be started when the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] is deployed. <br /> <br />|
   |**Password** <br /> <br />|Enter the username password that can retrieve files from the FTP server. <br /> <br />|
   |**Server Address** <br /> <br />|Enter the name of the FTP server or the IP address. <br /> <br />|
   |**Server Port** <br /> <br />|Enter the FTP server port. Default is 21 and is typically used for FTP. <br /> <br />|
   |**Use SSL** <br /> <br />|Select **True** if the connection to the FTP server must use SSL. For this tutorial, select **False**. <br /> <br />|
   |**Username** <br /> <br />|Enter the username that can retrieve files from the FTP server. <br /> <br />|

## See Also
[Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server](/Topic/Tutorial__Using_BizTalk_Bridges_to_Insert_Flat_File_Messages_into_an_On-premises_SQL_Server.md)

