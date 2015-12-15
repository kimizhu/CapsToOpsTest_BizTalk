---
description: na
keywords: na
pagetitle: Step 4: Add an FTP Source
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-03
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 006ffe2d-d5e5-4fd2-b34c-3874ed038e77
---
# Step 4: Add an FTP Source
In this step, you add an FTP source to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. An FTP source component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface represents a location on the FTP Server where Northwind Traders drops the flat-file message to send to Humongous Insurance.

> [!NOTE]
> The FTP Server from where a bridge picks a message must be in a public domain and must allow connections in either secure (SSL) or non-secure mode.

### To add an FTP source

1. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] surface, right-click anywhere on [!INCLUDE[msgflow](/Token/msgflow_md.md)] surface, select **Properties** and update the **BizTalk Service URL** property to include your [!INCLUDE[af_integration](/Token/af_integration_md.md)] name. This is the name that you provided in [Azure classic portal](http://go.microsoft.com/fwlink/?LinkId=211879) while provisioning the [!INCLUDE[af_integration](/Token/af_integration_md.md)].

2. From the **Toolbox**, drag and drop an **FTP Source** component onto the surface.

3. Right-click the component and select **Properties**. The following table provides information about the properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Content Encoding** <br /> <br />|Specify the character encoding of the message. Default is **UTF8**. For this tutorial, retain the default. <br /> <br />|
   |**Content Type** <br /> <br />|Specify Text or XML as the message file type. Default is **Text**. For this tutorial, retain the default. <br /> <br />|
   |**Entity Name** <br /> <br />|Specify a unique and descriptive name of the FTP Source component. For this tutorial, specify **ClaimsSource**. <br /> <br />|
   |**File Mask** <br /> <br />|Specify a File Mask to filter the messages pulled from the FTP server. For this tutorial, enter **&#42;.txt**. <br /> <br />|
   |**Folder Path** <br /> <br />|Specify the folder on the FTP server that contains the messages to retrieve. For this tutorial, Humongous Insurance pulls all the messages from a **ReceiveFFMessage** folder on the FTP server. Hence, enter **ReceiveFFMessage**. <br /> <br />|
   |**FTP Transfer Mode** <br /> <br />|Specify **Binary** or **ASCII** as the mode of transfer. Default is **Binary**. For this tutorial, retain the default. <br /> <br />|
   |**Initial Status** <br /> <br />|Specify **Stop** or **Start** for the FTP Source. Default is **Start**. For this tutorial, retain the default. If set to **Start**, the FTP Source component is started when the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] is deployed. **Note:** If the initial status is set to **Stop**, you can set it to **Start** even after the project (which includes the bridge, artifacts, and the FTP source) has been deployed. [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides PowerShell cmdlets to start sources for a [!INCLUDE[bridge](/Token/bridge_md.md)].  For more information, see [Start-AzureBizTalkBridgeSource](/Topic/Start-AzureBizTalkBridgeSource.md). <br />|
   |**Password** <br /> <br />|Enter the username password that can retrieve files from the FTP server. <br /> <br />|
   |**Server Address** <br /> <br />|Enter the name or IP address of the FTP server. <br /> <br />|
   |**Server Port** <br /> <br />|Enter the FTP server port. Default is 21 and is typically used for FTP. <br /> <br />|
   |**Use SSL** <br /> <br />|Select **True** if the connection to the FTP server must use SSL. For this tutorial, select **False**. <br /> <br />|
   |**Username** <br /> <br />|Enter the username that can retrieve files from the FTP server. <br /> <br />|

4. Save changes to the project.

## See Also
[Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md)

