---
description: na
keywords: na
pagetitle: Configure an SFTP Destination
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d631c52b-31fb-4301-9e4b-94aed0a639e1
---
# Configure an SFTP Destination
Lists the steps to create an SFTP Destination in [!INCLUDE[azure_2](/Token/azure_2_md.md)][!INCLUDE[af_integration](/Token/af_integration_md.md)].

> [!NOTE]
> To successfully route messages to an SFTP Destination, the SFTP FileName must be added as a Route Action. This FileName can either be a promoted property from the SFTP Source or it could be hardcoded as an expression.

## Add an SFTP Destination

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. Steps at [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **SFTP**  component under **Route Destinations** to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area.

4. Right-click the component and select **Properties**. The following table provides information about the properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Entity Name** <br /> <br />|Specify a unique and descriptive name of the **SFTP Destination** component. <br /> <br />|
   |**Folder Path** <br /> <br />|Specify the folder on the SFTP server to put the messages.  For example, if you want to put all XML messages in the CustomerFiles\Contoso SFTP folder, enter **CustomerFiles\Contoso**. <br /> <br />|
   |**Password** <br /> <br />|Enter the username password that can put files on the SFTP server. <br /> <br />|
   |**Server Address** <br /> <br />|Enter the SFTP server name or IP address. <br /> <br />|
   |**Server Port** <br /> <br />|Enter the SFTP server port. Default is 22. <br /> <br />|
   |**Username** <br /> <br />|Enter the username that can put files on the SFTP server. <br /> <br />|

5. From the File menu, select **Save**

## Authentication

- **Server Authentication**: The SFTP Source and SFTP Destination trust all server certificates.

- **Client Authentication**: Enter a username and password that can get/put files on the SFTP computer folder. This is exactly the same as logging into an FTP server.

## Additional
SSH File Transfer Protocol (SFTP) is a common protocol used to securely transfer files between two external partners. SFTP has become one the preferred methods to transfer files. [!INCLUDE[af_integration](/Token/af_integration_md.md)] includes SFTP functionality that enables you to send messages to an SFTP server. This topic lists the steps to use an SFTP server as a message destination in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. Use this destination to push a message to a folder on an SFTP server.

The **SFTP Destination** component can be used as the destination to an [!INCLUDE[one-way](/Token/one-way_md.md)] or a [!INCLUDE[passthru](/Token/passthru_md.md)]. An **SFTP Destination** cannot be used a destination for [!INCLUDE[request_response](/Token/request_response_md.md)]. [Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md) provides details on how to configure these [!INCLUDE[bridge](/Token/bridge_md.md)]s. After you have added a bridge and the **SFTP Destination** component to the design area, select **Connector** from the Toolbox, and connect the **SFTP Destination** to the [!INCLUDE[bridge](/Token/bridge_md.md)].

## See Also
[Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md)

