---
description: na
keywords: na
pagetitle: Tutorial: Using BizTalk Service Bridges to Send and Receive Messages from Service Bus Relay Service
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14d7f8b8-074c-485f-a2f6-c9a02cc1779a
---
# Tutorial: Using BizTalk Service Bridges to Send and Receive Messages from Service Bus Relay Service
This tutorial provides instructions on how to send XML messages with different schemas to a single [!INCLUDE[bridge](/Token/bridge_md.md)] endpoint deployed using [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. The [!INCLUDE[bridge](/Token/bridge_md.md)] processes the message and routes them to more than one relay services based on the business logic defined as part of the solution. Using this scenario, the tutorial also showcases other capabilities of [!INCLUDE[af_integration](/Token/af_integration_md.md)] such as:

- **Route Filters**: The [!INCLUDE[bridge](/Token/bridge_md.md)] enables you to route messages to the intended recipient based on filters. The filters are set on certain values that are passed as part of the message. For example, if the value in the element **&lt;Recipient&gt;** in the XML message is set to **Finance**, send the message to **Service A**. Otherwise, send the message to **Service B**. For more information, see [The Routing Condition](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_Filter).

- **Route Action**: Route actions help in bridging protocol mismatch. For example, consider two applications, **App A** and **App B**. **App A** sends messages by using the REST protocol while **App B** receives only SOAP messages. If **App A** sends the message to the [!INCLUDE[bridge](/Token/bridge_md.md)] instead, the [!INCLUDE[bridge](/Token/bridge_md.md)] includes SOAP headers on the message as part of Route Action. The [!INCLUDE[bridge](/Token/bridge_md.md)] then sends the message over to **App B**. For more information, see [The Routing Action](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_RoutingAction).

- **Reply Action**: Reply Action provides the same capability while sending a response back to the client, that Route action provides while sending a message to the receiver. So, if **App B** sends a response to **App A**, [!INCLUDE[bridge](/Token/bridge_md.md)]s use the **Reply Action** capabilities to stamp the response with headers that the client requires. For more information, see the [Reply Action](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md#BKMK_Send).

This tutorial demonstrates these capabilities of the [!INCLUDE[bridge](/Token/bridge_md.md)], in addition to other, using a business scenario.

## <a name="BKMK_Scenario"></a>Business Scenario
Northwind Traders is an automobile insurance company. Northwind Traders receive request for new policy quotes in an XML format compliant with the standard ACORD schema, an industry standard for insurance messages. The incoming messages can be in any ACORD-compliant format. So, Northwind Traders must configure a solution that can process XML messages that conform to more than one XML schema. After Northwind Traders receive the message, it is validated against the provided ACORD message schemas and transformed into a schema internal to Northwind. Northwind then sends the message to a backend service that processes the message further. However, there are certain routing conditions before the message is sent to the service.

- If the quote amount in the message is less than $10000, it must be sent to a relay service, say **RelayReceiverServiceA**. Before sending the message to the relay service, a SOAP header called **QuoteType** must be added to the message header. The value of this header must be set to **SmallAmounts**.

- If the quote amount in the message is greater than $10000, it is treated as a high-risk claim and is sent to another relay service, say **RelayReceiverServiceB**. Before sending the message to the service, a SOAP header called **QuoteType** must be added to the message header. The value of the header must be set to **LargeAmounts**.

After receiving the message the services generate a response, add headers, and send a response back to the [!INCLUDE[bridge](/Token/bridge_md.md)]. The services add the following headers:

|Response from service <br /> <br />|Headers added <br /> <br />|
|-------------------------|-----------------|
|RelayServiceA <br /> <br />|MsgStatus - Success <br /> <br />Eligibility - ApprovedForSmallAmounts <br /> <br />|
|RelayServiceB <br /> <br />|MsgStatus - Success <br /> <br />Eligibility - ApprovedForLargeAmounts <br /> <br />|
The response from the service is in the same format as the Northwind’s internal request format. After the [!INCLUDE[bridge](/Token/bridge_md.md)] receives the response, it transforms it to the response message schema compliant with ACORD standards. The [!INCLUDE[bridge](/Token/bridge_md.md)] also extracts the value from the **MsgStatus** header and assigns it to an element in the response schema. Finally, before sending the message back to the client, the [!INCLUDE[bridge](/Token/bridge_md.md)] adds another header called **ProcessingStatus** and sets its value to **Complete**. The following illustration represents this scenario.

![](/Image/BridgesSvc_Scenario.gif)

## How to Achieve the Scenario Using [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]
Northwind Traders use [!INCLUDE[af_integration](/Token/af_integration_md.md)] to set up this scenario. Here’s what Northwind Traders do at their end for this scenario to work end-to-end:

- Northwind creates two relay services, **RelayReceiverServiceA** and **RelayReceiverServiceB**. **RelayReceiverServiceA** receives messages with quote amount less than $10000. **RelayServiceB** receives messages with quote amount greater than $10000. After receiving the message, both the services generate a response message and stamp it with the headers, as described in the business scenario.

- Northwind creates a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and adds a [!INCLUDE[request_response](/Token/request_response_md.md)] to process the incoming XML messages and send a response. Northwind also adds two-way relay service components, one each for **RelayReceiverServiceA** and **RelayReceiverServiceB**.

- Northwind adds all the required artifacts (schemas and transforms) to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

- Northwind configures the *request* path of the [!INCLUDE[request_response](/Token/request_response_md.md)] to do the following:

   - Configures the **Validate** stage to validate the XML messages against the ACORD schemas.

   - Configures the **Enrich** stage to promote properties based on which the messages are routed to the backend services.

   - Configures The **Transform** stage to transform messages from the ACORD schema to Northwind’s internal schema.

- Northwind configures the *response* path of the [!INCLUDE[request_response](/Token/request_response_md.md)] to do the following:

   - Configures the **Enrich** stage to extract the **MsgStatus** header that the relay services added to the response message.

   - Configures the **[!INCLUDE[transform](/Token/transform_md.md)]** stage to transform the response from the relay services into a message schema compliant with ACORD standards. In this stage, the [!INCLUDE[bridge](/Token/bridge_md.md)] also assigns the value from the **MsgStatus** header into an element in the response schema.

   - Configures the **Reply Action** to include the **ProcessingStatus** header in the response message that is sent to the client.

- Northwind adds two external relay endpoints to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] representing the two relay services and connects them to the [!INCLUDE[request_response](/Token/request_response_md.md)] bridge. As part of these routing connectors, Northwind does the following:

   - Connects all the components on the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface and sets the filter conditions based on the quote amount.

   - Stamps the **QuoteType** header on the message and sets its value to either **SmallAmounts** or **LargeAmounts** depending on which service the message is being routed to.

- Finally, Northwind deploys the two relay service on [!INCLUDE[sb2](/Token/sb2_md.md)] and the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] to [!INCLUDE[af_integration](/Token/af_integration_md.md)] and sends a message to the [!INCLUDE[bridge](/Token/bridge_md.md)] endpoint.

## How to Use This Tutorial
This tutorial is written around a sample, **Bridges_RelayServices.zip**, which is available as part of the download from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=252395). You could use the sample and go through this tutorial to understand how the sample was built. Or, you could use this tutorial to create your own application. This tutorial is targeted towards the second approach so that you understand how this application was built. Also, as much as possible, the tutorial is consistent with the sample and uses the same names for artifacts (for example, schemas, transforms) as used in the sample.

Even though Microsoft recommends that you follow the tutorial to understand the concepts and procedures, do the following if you wish to use the sample:

- Download the **Bridges_RelayServices** sample and make relevant changes like providing your [!INCLUDE[sb2](/Token/sb2_md.md)] namespace, issuer name, issuer key. After making the required changes, build and deploy the application.

- Build and host the two relay services to accept request messages received via the [!INCLUDE[bridge](/Token/bridge_md.md)].

- Use the **MessageSender** tool provided with the package to send request messages to the [!INCLUDE[bridge](/Token/bridge_md.md)]. Look at the command prompts for the services as well as the **MessageSender** tool to see if the messages were processed successfully. If the messages are successfully processed, the request and response schemas are saved under the project’s \bin\Debug folder. The location and name of the message files are also displayed on the respective command prompts.

## Set Up Your Computer
From the [!INCLUDE[af_integration](/Token/af_integration_md.md)] download location ([http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)), download and install the [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK. For instructions, see [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md). Installing the SDK installs the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] template in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)]. This project template is used to create [!INCLUDE[bridge](/Token/bridge_md.md)]s that validate, [!INCLUDE[transform](/Token/transform_md.md)], and route messages to different endpoints as described in the business scenario.

## In This Section

- [Step 1: Build and Deploy the Relay Services](/Topic/Step_1__Build_and_Deploy_the_Relay_Services.md)

- [Step 2: Create the BizTalk Service Project](/Topic/Step_2__Create_the_BizTalk_Service_Project.md)

- [Step 3: Add Artifacts to the Project](/Topic/Step_3__Add_Artifacts_to_the_Project.md)

- [Step 4: Configure a Request-Reply Bridge](/Topic/Step_4__Configure_a_Request-Reply_Bridge.md)

- [Step 5: Connect Bridge and Services](/Topic/Step_5__Connect_Bridge_and_Services.md)

- [Step 6: Deploy the XML Request-Reply Bridge](/Topic/Step_6__Deploy_the_XML_Request-Reply_Bridge.md)

- [Step 7: Test the Solution](/Topic/Step_7__Test_the_Solution.md)

## See Also
[Tutorials and Samples](/Topic/Tutorials_and_Samples.md)

