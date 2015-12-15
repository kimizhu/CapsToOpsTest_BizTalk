---
description: na
keywords: na
pagetitle: Include a Service Bus Queue Destination
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 610405c1-ab48-4d93-9dd8-13f4ec45bffd
---
# Include a Service Bus Queue Destination
Add a [!INCLUDE[sb2](/Token/sb2_md.md)] queue as a destination to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

> [!IMPORTANT]
> In a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], you can represent [!INCLUDE[sb2](/Token/sb2_md.md)] queue destinations that have still not been created. However, representing a non-existent [!INCLUDE[sb2](/Token/sb2_md.md)] queue on a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] designer area does not create the queue.

### To add a [!INCLUDE[sb2](/Token/sb2_md.md)] queue to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md) lists the steps.

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. **BizTalk Service URL**, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **[!INCLUDE[sb2](/Token/sb2_md.md)] Queue Destination** to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area.

4. Right-click the [!INCLUDE[sb2](/Token/sb2_md.md)] Queue component, and then select **Properties**. Enter the following properties:

   |Property Name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |**Associated Project Item** <br /> <br />|This is a read-only field and provides the name of the associated .config file. If you change the name of the component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area by changing the **Entity Name** property, the name of the .config file also changes. <br /> <br />|
   |**Authentication** <br /> <br />|Enter how you want to authenticate with the [!INCLUDE[sb2](/Token/sb2_md.md)] Queue. Click the ellipsis **(…)** next to the **Authentication** property and then select a value from the **Token Provider** drop-down. <br /> <br /><ul><li>Select **Shared Secret**, and then enter the issuer name and issuer key. </li><li>Select **Shared Access Signature** (SAS), and then enter the key name and key value associated with the SAS. </li> </ul>|
   |**Endpoint Configuration Name** <br /> <br />|Name of the client endpoint configuration in the .config file that defines which encoding to use. Options are **TextEncodedMessageBody** and **BinaryEncodedSoapEnvelope**. Use **TextEncodedMessageBody** when the receiver is a thick client or REST-based. Use **BinaryEncodedSoapEnvelope** if the receiver is a WCF service. <br /> <br />|
   |**Entity Name** <br /> <br />|The name of the queue component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area. This name should be unique for a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. **Important:** The entity name for a [!INCLUDE[sb2](/Token/sb2_md.md)] Queue must only contain alphanumeric characters. <br />|
   |**Runtime Address** <br /> <br />|The public runtime endpoint URL where the [!INCLUDE[sb2](/Token/sb2_md.md)] Queue is deployed. Update this field to include your [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. <br /> <br />|

5. Click **Save**.

## How to Read a Message from a Queue
In scenarios where a message flows from a [!INCLUDE[bridge](/Token/bridge_md.md)] to a [!INCLUDE[sb2](/Token/sb2_md.md)] Queue, you can read the message from the Queue either as REST or SOAP. For REST, you can use the following code snippet to read the message:

```
BrokeredMessage brmsg; 
Stream actualStream = brmsg.GetBody(); 
XmlReader actualReader = XmlReader.Create(actualStream); 
Message msg = Message.CreateMessage(MessageVersion.Default, "*", actualReader);
```
For SOAP, you could read the message as a WCF message. For a sample, see the WCF Channel Session sample at [http://go.microsoft.com/fwlink/p/?LinkId=237002](http://go.microsoft.com/fwlink/p/?LinkId=237002).

## See Also
[Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md)

