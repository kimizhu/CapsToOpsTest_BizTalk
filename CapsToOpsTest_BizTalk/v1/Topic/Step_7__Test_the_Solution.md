---
description: na
keywords: na
pagetitle: Step 7: Test the Solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 772f33e5-29a8-4870-b99a-c3933670e67d
---
# Step 7: Test the Solution
This topic in the tutorial lists the steps to test the solution by sending messages with different quote amounts to the endpoint where the [!INCLUDE[request_response](/Token/request_response_md.md)] is deployed. The tutorial uses the **MessageSender** tool to send messages to the endpoint. The tool is available with the sample package is available at [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=252395).

The solution must be tested by sending messages with different schemas and messages that have quote amount less than or greater than $10000. So, the **SampleData** folder within the package includes the following sample request messages that you can use to test the solution.

TABLE REMOVED

### To send a message to the [!INCLUDE[bridge](/Token/bridge_md.md)]

1. Locate the **MessageSender** project in the sample package and build it.

2. Use the resulting **MessageSender** command-line executable (under \bin\Debug folder within the project) to send messages to the deployed [!INCLUDE[bridge](/Token/bridge_md.md)] endpoint. This tool accepts command-line parameter in the following format:

   ```
   MessageSender.exe <ACSNamespace> <IssuerName> <IssuerKey> <RuntimeAddress> <MessageFilepath> <ContentType>
   ```
   Where,

   TABLE REMOVED

   Open a command prompt and navigate to the solution where you built the **MessageSender** project. Run the following command to send the request message that has quote amount less than $10000:

   ```
   MessageSender.exe <ACSNamespace> owner <issuer key>https://<biztalk_deployment_url>.biztalk.windows.net/default/ServiceBridge<path to the samples>\Bridges_RelayServices\SampleData\ACORDR1_RequestMessage_SmallAmount.xml "application/soap+xml"
   ```

3. Because **RelayReceiverServiceA** processes messages with quote amounts less than $10000, go to the command prompt for the service. If the service receives the message successfully, you must see the following message displayed on the console:

   ```
   *************************************************************************
   Message processed successfully. Request message saved at : 
   C:\Tutorial\Lessons\Bridges_RelayServices\RelayReceiverServiceA\bin\Debug\Received_Message<unique_number>.xml
   *************************************************************************
   ```
   The text indicates that the service received the message from the [!INCLUDE[bridge](/Token/bridge_md.md)] and that the message is saved at the given location. Go to the location where the message is saved and open the message XML file. Notice that the message includes the following header:

   ```
   <QuoteType xmlns="http://Northwind.com/insurance/ACORD1/xml/">SmallAmounts</QuoteType>
   ```
   You had configured the [!INCLUDE[bridge](/Token/bridge_md.md)] to add the **QuoteType** custom header in the section [Include Custom Headers in the Message](/Topic/Step_5__Connect_Bridge_and_Services.md#BKMK_RouteAction).

4. Now, send the request message where quote amount is greater than $10000. Type the following on the **MessageSender** command prompt:

   ```
   MessageSender.exe <ServiceBusNamespace> owner <issuer key>https://<ServiceBusNamespace>.servicebus.windows.net/ServiceBridge<path to the samples>\Bridges_RelayServices\SampleData\ACORDR1_RequestMessage_LargeAmount.xml "application/soap+xml"
   ```
   Because **RelayReceiverServiceB** processes messages with quote amounts less than $10000, go to the command prompt for the service. If the service receives the message successfully, you must see the following message displayed on the console:

   ```
   *************************************************************************
   Message processed successfully. Request message saved at :
   C:\Tutorial\Lessons\Bridges_RelayServices\RelayReceiverServiceB\bin\Debug\Received_Message<unique_number>.xml
   *************************************************************************
   ```
   Once again, go to the location where the request message is saved. This time, notice that the value of the **QuoteType** header is set to **LargeAmounts**.

   ```
   <QuoteType xmlns="http://Northwind.com/insurance/ACORD1/xml/">LargeAmounts</QuoteType>
   ```

5. In both the cases, whether you send a request message with a smaller quote amount or a larger quote amount, a message is displayed on the **MessageSender** console as well:

   ```
   Sending data to end point: https://<biztalk_deployment_url>.biztalk.windows.net/default/ServiceBridge
   Tracking ID for the message sent is <tracking ID>
   Message sent successfully
   Received response
   ********************************************************************************
   Received a response message from the bridge. The message is saved at : 
   C:\Tutorial\Lessons\Bridges_RelayServices\MessageSender\MessageSender\bin\Debug\Response_Message<unique_number>.xml
   ********************************************************************************
   ```
   Go to the location where the response messages are saved and open the two messages. Notice the following in the two messages:

   - Both the response messages have the **MsgStatusCd** element in the message body and its value is set to **Success**.

      ```
      <ns1:MsgStatusCd>Success</ns1:MsgStatusCd>
      ```
      You had extracted this value from the response message header and passed it on to the response message body as part of the procedure [To extract and promote properties in the pre-transform Enrich stage](/Topic/Step_4_b):%20Configure%20the%20Response%20Bridge.md#BKMK_ResP_Enrich).

   - Both the response messages have the following header included:

      ```
      <ProcessingStatus xmlns="http://Northwind.com/insurance/ACORD1/xml/">Complete</ProcessingStatus>
      ```
      You had configured the [!INCLUDE[bridge](/Token/bridge_md.md)] to add this custom header in the section [To configure the reply action](/Topic/Step_4_b):%20Configure%20the%20Response%20Bridge.md#BKMK_Reply).

   - Finally, both the response messages have two other custom headers as well, **MsgStatus** and **Eligibility**. The relay service adds these headers as part of the response message. While the value of **MsgStatus** is set to **Success** in responses from both the services, the value of **Eligibility** varies depending on which service sent the response:

      TABLE REMOVED

      Because both the responses are sent back the same message sender client, you can use the **Eligibility** header to determine whether the response came from **RelayReceiverServiceA** or **RelayReceiverServiceB**.

6. Repeat steps 2 and 3 by sending messages that are compliant with ACORDRq2.xsd. In the response messages that the client receives, notice that an additional node (**Comments**) is included. You configured the [!INCLUDE[bridge](/Token/bridge_md.md)] to extract this element from the request message in the procedure [To extract and promote properties in the pre-transform Enrich stage](/Topic/Step_4_a):%20Configure%20the%20Request%20Bridge.md#BKMK_ReqP_Enrich) and then configured the [!INCLUDE[transform](/Token/transform_md.md)] to pass the extracted value to the response message in the procedure [To map NorthwindSchema.xsd to ACORDRs2.xsd](/Topic/Step_3__Add_Artifacts_to_the_Project.md#BKMK_TransformRes2).

## See Also
[Tutorial: Using BizTalk Service Bridges to Send and Receive Messages from Service Bus Relay Service](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md)

