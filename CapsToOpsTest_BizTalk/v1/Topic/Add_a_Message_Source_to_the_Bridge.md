---
description: na
keywords: na
pagetitle: Add a Message Source to the Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d63ef53-1ef7-4110-8f65-f5c24cb8b886
---
# Add a Message Source to the Bridge
Use [!INCLUDE[af_integration](/Token/af_integration_md.md)] to receive messages from FTP, SFTP, [!INCLUDE[sb2](/Token/sb2_md.md)] Queue, and [!INCLUDE[sb2](/Token/sb2_md.md)] topic subscription. These ‘sources’ are in addition to sending and receiving messages to and from HTTP endpoints. This topic lists the topics to add and configure the sources from where a [!INCLUDE[bridge](/Token/bridge_md.md)] can receive messages.

> [!NOTE]
> The sources can be used as a message source for an [!INCLUDE[one-way](/Token/one-way_md.md)] or a [!INCLUDE[passthru](/Token/passthru_md.md)]. These sources cannot be used a source for [!INCLUDE[request_response](/Token/request_response_md.md)].

In this topic:

[Add an FTP Source](/Topic/Add_a_Message_Source_to_the_Bridge.md#BKMK_AddFTP)

[Add an SFTP Source](/Topic/Add_a_Message_Source_to_the_Bridge.md#BKMK_AddSFTP)

[Add a queue source](/Topic/Add_a_Message_Source_to_the_Bridge.md#BKMK_AddQueue)

[Add a subscription source](/Topic/Add_a_Message_Source_to_the_Bridge.md#BKMK_AddSubscription)

These steps assume you’ve created [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. See [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

## <a name="BKMK_AddFTP"></a>Add an FTP Source
> [!NOTE]
> You can explicitly start or stop the FTP source (which controls polling of the FTP location) without requiring the configuration of the bridge to be changed.

1. Open your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **FTP Source** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area.

4. Right-click the component and select **Properties**. The following table describes these properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Content Encoding** <br /> <br />|Enter the character encoding of the message. Default is UTF8. Options include: <br /> <br /><ul><li>UTF8 </li><li>UTF16 </li><li>UTF16BE </li><li>ASCII </li> </ul>|
   |**Content Type** <br /> <br />|Enter Text or XML as the message file type. Default is Text. <br /> <br />|
   |**Entity Name** <br /> <br />|Enter a unique and descriptive name of the FTP Source component. <br /> <br />|
   |**File Mask** <br /> <br />|Enter a File Mask to filter the messages pulled from the FTP server. For example, if you want to pull all XML messages, enter **&#42;.xml**. <br /> <br />|
   |**Folder Path** <br /> <br />|Enter the folder on the FTP server that contains the messages to retrieve.  For example, if you want to pull all XML messages in the CustomerFiles\Contoso FTP folder, enter **CustomerFiles\Contoso**. <br /> <br />|
   |**FTP Transfer Mode** <br /> <br />|Enter Binary or ASCII as the Transfer Mode. Default is Binary. For example, if the messages only contain text-type of data, select ASCII. If the messages contain any type of data, select Binary. <br /> <br />|
   |**Initial Status** <br /> <br />|Enter Stop or Start for the FTP Source. Default is Start. For example, if you want the FTP Source component to be started when the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] is deployed, select Start. **Note:** If you set the initial status to stop, you can later start the source using the PowerShell cmdlet. For more information, see [Start-AzureBizTalkBridgeSource](/Topic/Start-AzureBizTalkBridgeSource.md). <br />|
   |**Password** <br /> <br />|Enter the username password that can retrieve files from the FTP server. <br /> <br />|
   |**Server Address** <br /> <br />|Enter the FTP server name or IP address. <br /> <br />|
   |**Server Port** <br /> <br />|Enter the FTP server port. Default is 21 and is typically used for FTP. <br /> <br />|
   |**Use SSL** <br /> <br />|Select True if the connection to the FTP server must use SSL. <br /> <br />|
   |**Username** <br /> <br />|Enter the username that can retrieve files from the FTP server. <br /> <br />|

5. From the File menu, select **Save**

[Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md) provides details on how to configure these [!INCLUDE[bridge](/Token/bridge_md.md)]s. After you have added a bridge and the **FTP Source** component to the design area, select **Connector** from the Toolbox and connect the **FTP Source** to the [!INCLUDE[bridge](/Token/bridge_md.md)].

> [!NOTE]
> A bridge deployed in [!INCLUDE[af_integration](/Token/af_integration_md.md)] can only receive messages from an FTP server hosted in a public domain.

## <a name="BKMK_AddSFTP"></a>Add an SFTP Source
> [!NOTE]
> You can explicitly start or stop the SFTP source (which controls polling of the SFTP location) without requiring the configuration of the bridge to be changed.

An SFTP Source polls a folder on an SFTP computer. Steps to create an SFTP Source:

1. Open your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **SFTP Source** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area.

4. Right-click the component and select **Properties**. The following table describes these properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Content Type** <br /> <br />|Enter Text or XML as the message file type. Default is Text. <br /> <br />|
   |**Encoding** <br /> <br />|Enter the content encoding. Options include: <br /> <br /><ul><li>UTF8 </li><li>UTF16 </li><li>UTF16BE </li><li>ASCII </li> </ul>|
   |**Entity Name** <br /> <br />|Enter a unique and descriptive name of the SFTP Source component. <br /> <br />|
   |**File Mask** <br /> <br />|Enter a File Mask to filter the messages pulled from the SFTP server. For example, if you want to pull all XML messages, enter **&#42;.xml**. <br /> <br />|
   |**Folder Path** <br /> <br />|Enter the folder on the SFTP server that contains the messages to retrieve.  For example, if you want to pull all XML messages in the CustomerFiles\Contoso SFTP folder, enter **CustomerFiles\Contoso**. <br /> <br />|
   |**Initial Status** <br /> <br />|Enter Stop or Start for the SFTP Source. Default is Start. When set to Start, the SFTP Source is polled for new files. <br /> <br />If you want to poll the SFTP Source when the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] is deployed, set to Start. **Note:** If you set the initial status to stop, you can later start the source using the PowerShell cmdlet. For more information, see [Start-AzureBizTalkBridgeSource](/Topic/Start-AzureBizTalkBridgeSource.md). <br />|
   |**Password** <br /> <br />|Enter the username password that can retrieve files from the SFTP server. <br /> <br />|
   |**Server Address** <br /> <br />|Enter the SFTP server name or IP address. <br /> <br />|
   |**Server Port** <br /> <br />|Enter the SFTP server port. Default is 22. <br /> <br />|
   |**Username** <br /> <br />|Enter the username that can retrieve files from the SFTP server. <br /> <br />|

5. From the File menu, select **Save**

**Authentication**

- **Server Authentication**: The SFTP Source and SFTP Destination trust all server certificates.

- **Client Authentication**: Enter a username and password that can get/put files on the SFTP computer folder. This is exactly the same as logging into an FTP server.

SSH File Transfer Protocol (SFTP) is a common protocol used to securely transfer files between two external partners. SFTP has become one the preferred methods to transfer files. [!INCLUDE[af_integration](/Token/af_integration_md.md)] includes SFTP functionality that enables you to receive messages from an SFTP source. This topic lists the steps to use an SFTP server as a message source in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. Use this source to pull a message from an SFTP server.

[Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md) provides details on how to configure these [!INCLUDE[bridge](/Token/bridge_md.md)]s. After you have added a bridge and the **SFTP Source** component to the design area, select **Connector** from the Toolbox, and connect the **SFTP Source** to the [!INCLUDE[bridge](/Token/bridge_md.md)].

## <a name="BKMK_AddQueue"></a>Add a queue source

1. Open your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **[!INCLUDE[sb2](/Token/sb2_md.md)] Queue Source** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] desiger.

4. Right-click the component and select **Properties**. The following table provides information about the properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Connection String** <br /> <br />|Enter the connection string for the queue. The connection string is available from the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414). <br /> <br />|
   |**Entity Name** <br /> <br />|Enter a unique and descriptive name of the queue source. <br /> <br />|
   |**Initial Status** <br /> <br />|Enter Stop or Start for the queue source. Default is Start. For example, if you want the queue source component to be started when the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] is deployed, select **Start**. **Note:** If you set the initial status to stop, you can later start the source using the PowerShell cmdlet. For more information, see [Start-AzureBizTalkBridgeSource](/Topic/Start-AzureBizTalkBridgeSource.md). <br />|
   |**Queue Name** <br /> <br />|Name of the queue that you must have already created under your [!INCLUDE[sb2](/Token/sb2_md.md)] namespace in the [!INCLUDE[azportal](/Token/azportal_md.md)] <br /> <br />|

5. From the File menu, select **Save**.

[Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md) provides details on how to configure these [!INCLUDE[bridge](/Token/bridge_md.md)]s. After you have added a bridge and the **[!INCLUDE[sb2](/Token/sb2_md.md)] Queue Source** component to the design area, select **Connector** from the Toolbox and connect the source to the [!INCLUDE[bridge](/Token/bridge_md.md)].

## <a name="BKMK_AddSubscription"></a>Add a subscription source

1. Open your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area and select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **[!INCLUDE[sb2](/Token/sb2_md.md)] Subscription Source** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area.

4. Right-click the component and select **Properties**. The following table lists the properties:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |**Connection String** <br /> <br />|Enter the connection string for the topic. The connection string is available from the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414). <br /> <br />|
   |**Entity Name** <br /> <br />|Enter a unique and descriptive name of the subscription source. <br /> <br />|
   |**Initial Status** <br /> <br />|Enter Stop or Start for the subscription source. Default is Start. For example, if you want the subscription source component to be started when the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] is deployed, select **Start**. **Note:** If you set the initial status to stop, you can later start the source using the PowerShell cmdlet. For more information, see [Start-AzureBizTalkBridgeSource](/Topic/Start-AzureBizTalkBridgeSource.md). <br />|
   |**Subscription Name** <br /> <br />|Name of the subscription that you must have already created for the topic, for which you specified the connection string earlier. This should be specified in the format *[TopicPath]/subscriptions/[SubscriptionName]*. <br /> <br />|

5. From the File menu, select **Save**.

[Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md) provides details on how to configure these [!INCLUDE[bridge](/Token/bridge_md.md)]s. After you have added a bridge and the **[!INCLUDE[sb2](/Token/sb2_md.md)] Subscription Source** component to the design surface, select **Connector** from the Toolbox and connect the source to the [!INCLUDE[bridge](/Token/bridge_md.md)].

## See Also
[Create Rich Messaging Endpoints on Azure](/Topic/Create_Rich_Messaging_Endpoints_on_Azure.md)

