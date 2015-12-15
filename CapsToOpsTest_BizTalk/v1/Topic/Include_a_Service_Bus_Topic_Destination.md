---
description: na
keywords: na
pagetitle: Include a Service Bus Topic Destination
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e11c136f-e5b7-4223-baac-a5619bf8809b
---
# Include a Service Bus Topic Destination
Add a [!INCLUDE[sb2](/Token/sb2_md.md)] topic as a destination to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

> [!IMPORTANT]
> In a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], you can represent [!INCLUDE[sb2](/Token/sb2_md.md)] topic destinations that have still not been created. However, representing a non-existent [!INCLUDE[sb2](/Token/sb2_md.md)] topic on a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] designer surface does not create the topic.

### To add a [!INCLUDE[sb2](/Token/sb2_md.md)] topic to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], as described in [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **[!INCLUDE[sb2](/Token/sb2_md.md)] Topic Destination** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area.

4. Right-click the [!INCLUDE[sb2](/Token/sb2_md.md)] Topic component, and then select **Properties**. Enter the following properties:

   |Property Name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |**Associated Project Item** <br /> <br />|This is a read-only field and provides the name of the associated .config file. If you change the name of the component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area by changing the **Entity Name** property, the name of the .config file also changes. <br /> <br />|
   |**Authentication** <br /> <br />|Specify how you want to authenticate with the [!INCLUDE[sb2](/Token/sb2_md.md)] Topic. Select the ellipsis **(…)** against the **Authentication** property and the select a value from the **Token Provider** drop-down. <br /> <br /><ul><li>Select **Shared Secret**, and then provide the issuer name and issuer key. </li><li>Select **Shared Access Signature** (SAS), and then provide the key name and key value associated with the SAS. </li> </ul>|
   |**Endpoint Configuration Name** <br /> <br />|Name of the client endpoint configuration in the .config file that defines which encoding to use. The available options are **TextEncodedMessageBody** and **BinaryEncodedSoapEnvelope**. Use **TextEncodedMessageBody** when the receiver is a thick client or REST-based. Use **BinaryEncodedSoapEnvelope** if the receiver is a WCF service. <br /> <br />|
   |**Entity Name** <br /> <br />|The name of the Topic component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area. This name should be unique for a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. **Important:** The entity name for a [!INCLUDE[sb2](/Token/sb2_md.md)] Topic must only contain alphanumeric characters. <br />|
   |**Runtime Address** <br /> <br />|The public runtime endpoint URL where the [!INCLUDE[sb2](/Token/sb2_md.md)] Topic is deployed. Update this field to include your [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. <br /> <br />|

5. Select **Save**.

## See Also
[Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md)

