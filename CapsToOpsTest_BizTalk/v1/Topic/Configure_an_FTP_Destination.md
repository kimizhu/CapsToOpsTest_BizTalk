---
description: na
keywords: na
pagetitle: Configure an FTP Destination
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e31c2c85-ca11-47db-848a-2caca5a0d83d
---
# Configure an FTP Destination
Configure an FTP destination for sending messages from a [!INCLUDE[bridge](/Token/bridge_md.md)] to an FTP server. Just like the **FTP Source** component, the **FTP Destination** component can be used as the destination for an [!INCLUDE[one-way](/Token/one-way_md.md)] or a [!INCLUDE[passthru](/Token/passthru_md.md)]. An **FTP Destination** component cannot be used a destination for [!INCLUDE[request_response](/Token/request_response_md.md)]. [Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md) provides details on how to configure these [!INCLUDE[bridge](/Token/bridge_md.md)]s. Once you have added a **FTP Destination** component to the [!INCLUDE[msgflow](/Token/msgflow_md.md)] designer, select **Connector** from the **Toolbox** and connect the [!INCLUDE[bridge](/Token/bridge_md.md)] to the **FTP Destination** component.

> [!NOTE]
> A bridge deployed in [!INCLUDE[af_integration](/Token/af_integration_md.md)] can only send messages to an FTP server hosted in a public domain.

> [!NOTE]
> In order to successfully route messages to an FTP Destination, the FTP FileName must be added as a Route Action. This FileName can either be a promoted property from the FTP Source or it could be hardcoded as an expression.

[Tutorials and Samples](/Topic/Tutorials_and_Samples.md) provides some end-to-end scenarios.

### To add an FTP Destination to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], as described in [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **FTP Destination** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area.

4. Right-click the component and select **Properties**. The following table provides information about the properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Entity Name** <br /> <br />|Enter a unique and descriptive name of the FTP destination component. <br /> <br />|
   |**Folder Path** <br /> <br />|Enter the folder on the FTP server where the [!INCLUDE[bridge](/Token/bridge_md.md)] sends the message. For example, if you want to send a message to CustomerFiles\Contoso FTP folder, enter **CustomerFiles\Contoso**. <br /> <br />|
   |**Password** <br /> <br />|Enter the username password that can send files to an FTP server. <br /> <br />|
   |**Server Address** <br /> <br />|Enter the FTP server name or IP address. <br /> <br />|
   |**Server Port** <br /> <br />|Enter the FTP server port. Default is 21 and is typically used for FTP. <br /> <br />|
   |**Transfer Mode** <br /> <br />|Enter Binary or ASCII as the Transfer Mode. Default is Binary. For example, if the messages only contain text-type of data, select ASCII. If the messages contain any type of data, select Binary. <br /> <br />|
   |**Use SSL** <br /> <br />|Select True if the connection to the FTP server must use SSL. <br /> <br />|
   |**Username** <br /> <br />|Enter the username that can retrieve files from the FTP server. <br /> <br />|

5. From the File menu, select **Save**.

## See Also
[Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md)

