---
description: na
keywords: na
pagetitle: Step 4(b): Configure the Response Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e498d62-bcd2-447d-b209-bfc044b9f5f5
---
# Step 4(b): Configure the Response Bridge
As part of the response bridge of the [!INCLUDE[request_response](/Token/request_response_md.md)], the tutorial demonstrates the following tasks:

- **Configure the pre-[!INCLUDE[transform](/Token/transform_md.md)] Enrich stage** – In this stage, define the property that must be extracted and promoted within the response message. This property is used within the [!INCLUDE[bridge](/Token/bridge_md.md)] for processing the message, such as assigning values to elements in the response message.

- **Configure the [!INCLUDE[transform](/Token/transform_md.md)] stage** – In this stage, include the [!INCLUDE[transform](/Token/transform_md.md)]s defined in the previous steps to [!INCLUDE[transform](/Token/transform_md.md)] the response message from Northwind into ACORD-compliant response schemas.

- **Configure the Reply Action** – In this stage, stamp the response message with message headers right before it is sent back to the client that sent the original request message.

## Configure the Pre-[!INCLUDE[transform](/Token/transform_md.md)] Enrich Stage
According to the [Business Scenario](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md#BKMK_Scenario), the response message that the relay services send to the [!INCLUDE[bridge](/Token/bridge_md.md)] contains a message header called **MsgStatus** and its value is set to **Success**. The value of the **MsgStatus** header must be assigned to the **MsgStatusCd** element in the ACORD-compliant response schema. The following two steps must be performed to achieve it.

- In the **Enrich** stage, extract the value of the **MsgStatus** header in the response message and assign it to a property.

- Using the **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] in a [!INCLUDE[transform](/Token/transform_md.md)], assign the value from the property to the **MsgStatusCd** element in the response schema.

The second task is already completed in the procedures [To map NorthwindSchema.xsd to ACORDRs1.xsd](/Topic/Step_3__Add_Artifacts_to_the_Project.md#BKMK_TransformRes1) and [To map NorthwindSchema.xsd to ACORDRs2.xsd](/Topic/Step_3__Add_Artifacts_to_the_Project.md#BKMK_TransformRes2). The following procedure demonstrates how to perform the first task, which is to create a property with the name **MsgStatus** and set it to extract the value from the **MsgStatus** response message header.

#### To extract and promote properties in the pre-[!INCLUDE[transform](/Token/transform_md.md)] Enrich stage

1. In the response bridge of the [!INCLUDE[request_response](/Token/request_response_md.md)] configuration, select the **Enrich** activity within the pre-[!INCLUDE[transform](/Token/transform_md.md)]**Enrich** stage, and from the **Properties** window, select the ellipsis button **(…)** against **Property Definitions**.

2. In **Property Definitions**, select **Add** to open the **Add Property** dialog box. In **Add Property**, do the following:

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Source (Read From) <br /> <br />|Type <br /> <br />|Select **Soap** from the drop-down list. <br /> <br />|
   |Source (Read From) <br /> <br />|SOAP Header Namespace <br /> <br />|Enter the following namespace: <br /> <br />DELETED CODE <br /> <br />The value provided for the SOAP Header Namespace property is the namespace that the relay service sets on the message while sending the response back. <br /> <br />|
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|Set this property to the name of the header, which is **MsgStatus**. <br /> <br />|
   |Property (Write To) <br /> <br />|Property Name <br /> <br />|Set the name of the property to **MsgStatus**. So, the value from the **MsgStatus** header in the response message is passed on to the **MsgStatus** property. <br /> <br />|
   |Property (Write To) <br /> <br />|Data Type <br /> <br />|Set the data type to **string**. <br /> <br />|
   The **Add Property** dialog box resembles the following:

   ![](/Image/BridgesSvc_ResP_MsgStatus.gif)

   Select **OK** and then select **OK** again in the **Property Definitions** dialog box.

3. Save the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

## Configure the [!INCLUDE[transform](/Token/transform_md.md)] Stage in the Response bridge
The procedures ([To map NorthwindSchema.xsd to ACORDRs1.xsd](/Topic/Step_3__Add_Artifacts_to_the_Project.md#BKMK_TransformRes1) and [To map NorthwindSchema.xsd to ACORDRs2.xsd](/Topic/Step_3__Add_Artifacts_to_the_Project.md#BKMK_TransformRes2)) demonstrated how to create two [!INCLUDE[transform](/Token/transform_md.md)]s to map the response message from the relay services to the ACORD-compliant response message format. This step demonstrates how to add those [!INCLUDE[transform](/Token/transform_md.md)]s to the response bridge of the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration so that the [!INCLUDE[bridge](/Token/bridge_md.md)] uses the [!INCLUDE[transform](/Token/transform_md.md)]s to process the response message before sending it back to the client.

#### To enter [!INCLUDE[transform](/Token/transform_md.md)]s in a [!INCLUDE[bridge](/Token/bridge_md.md)]

1. In the [!INCLUDE[request_response](/Token/request_response_md.md)] configuration, select the **Xml Transform** activity within the **[!INCLUDE[transform](/Token/transform_md.md)]** stage, and from the **Properties** window, select the ellipsis button **(…)** against the **Maps** property.

2. The **Maps Selection** dialog box, by default, shows only those maps that have the destination schema same as the response schema you specified earlier. For this tutorial, because the [!INCLUDE[bridge](/Token/bridge_md.md)] must process and [!INCLUDE[transform](/Token/transform_md.md)] the internal Northwind schema to two ACORD-compliant response schemas, select both the [!INCLUDE[transform](/Token/transform_md.md)]s you created (one to [!INCLUDE[transform](/Token/transform_md.md)] NorthwindSchema.xsd to ACORDRs1.xsd and the other to [!INCLUDE[transform](/Token/transform_md.md)] NorthwindSchema.xsd to ACORDRs2.xsd).

   ![](/Image/BridgesSvc_ResP_Transform.gif)

3. In **Maps Selection**, select **OK**. The maps you added are listed under the **Selected Maps** box on the itinerary designer.

4. Save the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

## Configure the Reply Action
According to the [Business Scenario](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md#BKMK_Scenario), the response message sent back to the client must include a message header called **ProcessingStatus** and its value must be set to **Complete**. To achieve this through the [!INCLUDE[bridge](/Token/bridge_md.md)], use the **Reply Action** ‘stage’ in the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration. **Reply Action** adds headers to the message, before it finally exits the [!INCLUDE[bridge](/Token/bridge_md.md)]. These headers can either have a constant value or values from the properties that are already promoted in the **Enrich** stages. Because the value of the header must always be set to **Complete**, this section uses the option to enter a constant value for a message header.

#### To configure the reply action

1. In the response bridge of the [!INCLUDE[request_response](/Token/request_response_md.md)] configuration, select the **Reply Action** activity within the **Send Reply** box. From the **Properties** pane, select the ellipsis button **(…)** against the **Reply Action** property to open the **Reply Actions** dialog box.

2. In **Reply Actions**, select **Add** to open the **Add Reply Action** dialog box. In **Add Reply Action**, do the following:

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Property (Read From) <br /> <br />|Expression <br /> <br />|Enter the expression as **'Complete'**. **Important:** Always enter the value for an expression within single quotes. <br />|
   |Destination (Write To) <br /> <br />|Type <br /> <br />|Enter the message type as **SOAP**. <br /> <br />|
   |Destination (Write To) <br /> <br />|SOAP Header Namespace <br /> <br />|Enter the namespace of the custom SOAP header to which the value is assigned. For this tutorial, set the namespace to &#96;http://Northwind.com/insurance/ACORD1/xml/&#96; **Important:** This field is disabled if you select a standard header name from the **Identifier** drop-down list. <br />|
   |Destination (Write To) <br /> <br />|Identifier <br /> <br />|Specifies the name of message header property to which the value is assigned. According the business scenario, set this property to **ProcessingStatus**. <br /> <br />|
   ![](/Image/BridgesSvc_ResP_ReplyAction.gif)

   Select **OK** and then select **OK** again in the **Reply Actions** dialog box.

3. Save the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

## See Also
[Step 4: Configure a Request-Reply Bridge](/Topic/Step_4__Configure_a_Request-Reply_Bridge.md)

