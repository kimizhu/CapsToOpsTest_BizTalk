---
description: na
keywords: na
pagetitle: Step 4(a): Configure the Request Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4bf9e02-cac7-4bc8-b842-735294a240b8
---
# Step 4(a): Configure the Request Bridge
As part of the request bridge of the [!INCLUDE[request_response](/Token/request_response_md.md)], the tutorial demonstrates how to perform the following tasks:

- **Specify the request and response schemas** – In this stage, enter the following:

   - Request schemas that govern the request messages that the [!INCLUDE[bridge](/Token/bridge_md.md)] can process.

   - Response schemas that govern the structure of the response message that the [!INCLUDE[bridge](/Token/bridge_md.md)] sends back to the client.

- **Configure the pre-[!INCLUDE[transform](/Token/transform_md.md)] Enrich stage** – In this stage, define the properties that must be extracted and promoted within the request message. These properties are used within the [!INCLUDE[bridge](/Token/bridge_md.md)] or within the solution for processing the message, routing it to the destination services, and so on.

- **Configure the [!INCLUDE[transform](/Token/transform_md.md)] stage** – In this stage, include the [!INCLUDE[transform](/Token/transform_md.md)]s you defined in the previous steps to [!INCLUDE[transform](/Token/transform_md.md)] the ACORD-compliant request messages to messages in a schema compliant with Northwind’s requirements.

## Enter Request and Response Message Schemas
This section provides instructions on how to add a [!INCLUDE[bridge](/Token/bridge_md.md)] to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. The section also describes how to configure the **Validate** stage to ensure that the [!INCLUDE[bridge](/Token/bridge_md.md)] processes only those messages that conform to the ACORD request and response schemas.

#### To add request and response schemas to a [!INCLUDE[bridge](/Token/bridge_md.md)] configuration

1. In the **Bridges_Services** project, double-click the **.bcs** file to open the itinerary designer.

2. Right-click anywhere on the itinerary designer and select **Properties** and then for the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag-and-drop the **[!INCLUDE[request_response](/Token/request_response_md.md)]** component to the itinerary designer. As a result a .BridgeConfig file is added to the solution.

4. Right-click the **[!INCLUDE[request_response](/Token/request_response_md.md)]**, select **Properties**, set the [!INCLUDE[bridge](/Token/bridge_md.md)] entity name to **XMLBridge** and the relative address of the [!INCLUDE[bridge](/Token/bridge_md.md)] to **ServiceBridge**. As a result, the complete endpoint URL where the [!INCLUDE[bridge](/Token/bridge_md.md)] is deployed is shown in the **Runtime Address** property.

5. Double-click the [!INCLUDE[request_response](/Token/request_response_md.md)] component to open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface. You can now enter the type of request and response messages that the [!INCLUDE[bridge](/Token/bridge_md.md)] can process. To enter the message type, on the [!INCLUDE[request_response](/Token/request_response_md.md)] design surface, within the **Message Types** box, select the add icon [ ![](/Image/IntSvcs_Bridges_Add_Icon.gif) ] to open the **Message Type Picker** dialog box.

6. The **Message Type Picker** dialog box lists five schemas – two ACORD request schemas (ACORDRq1.xsd and ACORDRq2.xsd), two ACORD response schemas (ACORDRs1.xsd and ACORDRs2.xsd), and one schema that is in the Northwind’s proprietary format (NorthwindSchema.xsd). From the **Available message types** box, select the **ACORDRq1.xsd** schema for the request message and select the RIGHT ARROW icon [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ] to add the schema to the **Request Message Type** section. Similarly, select the **ACORDRs1.xsd** schema for the response message and select the RIGHT ARROW icon [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ] to add the schema to the **Response Message Type** section. Select **OK**.

   Repeat this step to add the remaining request (ACORDRq2.xsd) and response (ACORDRs2.xsd) schema and then select **OK** again. Make sure that you do not select **NorthwindSchema.xsd** for the request or response schemas.

   > [!TIP]
   > By default the **Message Type Picker** dialog box does not display the schema file names; it only displays the root node for each schema. In such a case, identifying the right schema can be difficult. So, to make sure that you select the right schema, move the mouse cursor over the schema to see a tooltip box. That box displays the schema file name.

   The **Message Types** box resembles the following:

   ![](/Image/BridgesSvc_ReqP_MsgTypes.gif)

7. Save the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

## Configure the Pre-[!INCLUDE[transform](/Token/transform_md.md)] Enrich Stage
In the **Enrich** stage, you promote properties that are used in the solution to perform further processing on the message or for routing the message to the destination. As per the business scenario, there are two requirements for promoting the properties.

- **To extract the value in the QuoteAmount element in the request message schema**: According to the [Business Scenario](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md#BKMK_Scenario), if the value for **QuoteAmount** is less than $10000, the message must be routed to **RelayServiceA**. Otherwise, it must be routed to **RelayServiceB**. So, in the **Enrich** stage, extract the value of the **QuoteAmount** and then later, while configuring how to route messages to the right service, use the extracted property value to specify the routing condition.

   > [!NOTE]
   > The value for **QuoteAmount** element must be extracted from both the request schemas, **ACORDRq1.xsd** and **ACORDRq2.xsd**.

- To extract the value in the **Comments** element in the request schema. In the section, [To map NorthwindSchema.xsd to ACORDRs2.xsd](/Topic/Step_3__Add_Artifacts_to_the_Project.md#BKMK_TransformRes2), the **Comments** property is used to enter a value to the **Comments** node in the response schema, even though the property isn’t defined yet. The following procedure demonstrates how to define the **Comments** property in the **Enrich** stage.

   > [!NOTE]
   > Extract the value for **Comments** element only from the **ACORDRq2.xsd** because the other request schema does not have the **Comments** node at all.

#### To extract and promote properties in the pre-[!INCLUDE[transform](/Token/transform_md.md)] Enrich stage

1. In the request bridge of the [!INCLUDE[request_response](/Token/request_response_md.md)] configuration, select the **Enrich** activity within the pre-[!INCLUDE[transform](/Token/transform_md.md)]**Enrich** stage. Then, from the **Properties** window, select the ellipsis button **(…)** against **Property Definitions**.

2. In **Property Definitions**, select **Add** to open the **Add Property** dialog box. In **Add Property**, do the following:

   TABLE REMOVED

   The **Add Property** dialog box resembles the following:

   ![](/Image/BridgesSvc_ReqP_QuoteAmount.gif)

   Select **OK**.

3. Repeat step 2 to extract the following properties in the **Enrich** stage:

   |Element name in the schema <br /> <br />|Extract from schema <br /> <br />|Set property name to <br /> <br />|Set data type to <br /> <br />|
   |------------------------------|-----------------------|------------------------|--------------------|
   |QuoteAmount <br /> <br />|ACORDRq2.xsd <br /> <br />|QuoteAmount <br /> <br />|long <br /> <br />|
   |Comments <br /> <br />|ACORDRq2.xsd <br /> <br />|Comments <br /> <br />|string <br /> <br />|
   Select **OK** in the **Property Definitions** dialog box.

4. Save the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

## Configure the [!INCLUDE[transform](/Token/transform_md.md)] Stage in the Request Bridge
The procedure [To map ACORDRq1.xsd and ACORDRq2.xsd to NorthwindSchema.xsd](/Topic/Step_3__Add_Artifacts_to_the_Project.md#BKMK_TransformReq) demonstrates how to create two [!INCLUDE[transform](/Token/transform_md.md)]s to map the request messages to the Northwind’s request message format. This step demonstrates how to include the [!INCLUDE[transform](/Token/transform_md.md)]s to the request bridge of the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration. The [!INCLUDE[bridge](/Token/bridge_md.md)] uses the [!INCLUDE[transform](/Token/transform_md.md)]s to process the message and then sends it to the relevant relay service.

#### To enter [!INCLUDE[transform](/Token/transform_md.md)]s in a [!INCLUDE[bridge](/Token/bridge_md.md)]

1. In the [!INCLUDE[request_response](/Token/request_response_md.md)] configuration, select the **Xml Transform** activity within the **[!INCLUDE[transform](/Token/transform_md.md)]** stage, and from the **Properties** window, select the ellipsis button **(…)** against the **Maps** property.

2. The **Maps Selection** dialog box, by default, shows only those maps that have the source schema same as the request schema you specified earlier. For this tutorial, because the [!INCLUDE[bridge](/Token/bridge_md.md)] must process and transform two request schemas, select both the [!INCLUDE[transform](/Token/transform_md.md)]s you created (one to [!INCLUDE[transform](/Token/transform_md.md)] ACORDRq1.xsd to NorthwindSchema.xsd and the other to [!INCLUDE[transform](/Token/transform_md.md)] ACORDRq2.xsd to NorthwindSchema.xsd).

   ![](/Image/BridgesSvc_ReqP_Transforms.gif)

3. In **Maps Selection**, select **OK**. The maps you added are listed under the **Selected Maps** box on the [!INCLUDE[bridge](/Token/bridge_md.md)] designer surface.

4. Save the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

## See Also
[Step 4: Configure a Request-Reply Bridge](/Topic/Step_4__Configure_a_Request-Reply_Bridge.md)

