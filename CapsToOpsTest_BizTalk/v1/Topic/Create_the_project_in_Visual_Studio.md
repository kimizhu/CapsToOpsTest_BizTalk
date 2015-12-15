---
description: na
keywords: na
pagetitle: Create the project in Visual Studio
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57f25980-f745-4e8e-8a7e-4e0e87877dd5
---
# Create the project in Visual Studio
[!INCLUDE[af_integration](/Token/af_integration_md.md)] enables you to:

- Create and manage [EDI, AS2, and EDIFACT Messaging &#40;Business to Business&#41;](/Topic/EDI,_AS2,_and_EDIFACT_Messaging__Business_to_Business).md)

- Configure [Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md) to receive and send messages

- Use [Learn and create Message Maps and Transforms](/Topic/Learn_and_create_Message_Maps_and_Transforms.md) to manipulate data

- [Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md), you can connect to on-premises LOB applications from the cloud

But how and where do we start creating solutions to achieve each of these business objectives?

- For business-to-business messaging using EDI, AS2, and EDIFACT, there is a [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal where you can add your trading partners and create agreements between them. See [Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md).

- You use the [!INCLUDE[af_integration](/Token/af_integration_md.md)] project system to create a part or all of a [!INCLUDE[af_integration](/Token/af_integration_md.md)] solution. The core element of any such solution is a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] — a collection of items such as [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]s, [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] component, [!INCLUDE[transform](/Token/transform_md.md)]s, and schemas that you can build and deploy to [!INCLUDE[azure_2](/Token/azure_2_md.md)]. These items are used together to configure an end-to-end message flow.

   For example, a message is sent to an [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)], which processes it and sends it over to the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] component, which updates the backend LOB application.

When you create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], you generally include one or more of the components from the following list. These components play specific roles in creating your solution:

- **Bridges**: Bridges are message mediation patterns that process the message as it is relayed from the client to the destination endpoint. As part of the message mediation, [!INCLUDE[bridge](/Token/bridge_md.md)]s also extract/promote properties that can be used for message routing/processing.

   See [What are Bridges?](/Topic/What_are_Bridges_.md) and [Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md).

- **Sources**: These represent the message sources from which a [!INCLUDE[bridge](/Token/bridge_md.md)] can receive messages. See [Add a Message Source to the Bridge](/Topic/Add_a_Message_Source_to_the_Bridge.md).

- **Destinations**: These represent the endpoints where the messages, processed by the [!INCLUDE[bridge](/Token/bridge_md.md)], are routed to. See [Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md).

- **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**: Provides connectivity from [!INCLUDE[af_integration](/Token/af_integration_md.md)] application to on-premises LOB applications such as [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)], SAP, Oracle, Siebel, and so on. See [Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md).

- **Schemas**: A schema describes the structure of an XML document. Schemas exchange information among applications within an organization or among trading partners.

- **[!INCLUDE[transform](/Token/transform_md.md)]s**: A [!INCLUDE[transform](/Token/transform_md.md)] maps data from one format to another. [!INCLUDE[transform](/Token/transform_md.md)]s present source schemas and destination schemas side-by-side and enable you to define mapping between data elements of different messages. See [Learn and create Message Maps and Transforms](/Topic/Learn_and_create_Message_Maps_and_Transforms.md).

## Prerequisites for Configuring a [!INCLUDE[af_integration](/Token/af_integration_md.md)] Application
You must meet the following prerequisites before you can start creating [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications:

- [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md) to start creating [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications, including extending the reach of your [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications to on-premises LOB applications like [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)], SAP, and so on.

- You must have a valid [!INCLUDE[ac2](/Token/ac2_md.md)] and [!INCLUDE[sb2](/Token/sb2_md.md)] namespace with credentials.

## In This Section

- [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md)

- [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md)

- [Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md)

- [Learn and create Message Maps and Transforms](/Topic/Learn_and_create_Message_Maps_and_Transforms.md)

- [Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md)

## See Also
[BizTalk Services](/Topic/BizTalk_Services.md)

