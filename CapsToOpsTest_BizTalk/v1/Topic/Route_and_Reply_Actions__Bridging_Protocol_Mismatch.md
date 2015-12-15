---
description: na
keywords: na
pagetitle: Route and Reply Actions: Bridging Protocol Mismatch
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b28ccb0-dd88-4fbc-a5c4-c3b797a901e8
---
# Route and Reply Actions: Bridging Protocol Mismatch
Protocol mismatch comes into play when the message sender and message receiver operate on different message protocols. In a typical [!INCLUDE[af_integration](/Token/af_integration_md.md)] scenario involving [!INCLUDE[bridge](/Token/bridge_md.md)]s, a message sender sends a message to the [!INCLUDE[bridge](/Token/bridge_md.md)]. The [!INCLUDE[bridge](/Token/bridge_md.md)] process the message and then sends it out to the message receiver. This means the protocol mismatch has to be bridged at two instances:

- First when the message is sent to the message receiver. This is applicable for both [!INCLUDE[one-way](/Token/one-way_md.md)] and [!INCLUDE[request_response](/Token/request_response_md.md)] because in both cases the message has to be sent to a message receiver. This is called **Route Action**.

- Second when the response message received from the message receiver is sent back to the message sender. This is applicable only in [!INCLUDE[request_response](/Token/request_response_md.md)] because only for this [!INCLUDE[bridge](/Token/bridge_md.md)] a response has to be sent back to the message sender. This is called **Reply Action**.

Both Route and Reply actions operate on the properties that you define in the **Enrich** stage.

## <a name="BKMK_Route"></a>Route Action
Let us consider a scenario to understand how Route action can be used to do a protocol mismatch. As per the scenario, a POX (Plain Old XML)/REST message has to be sent to a WCF service (that expects SOAP message) via an [!INCLUDE[one-way](/Token/one-way_md.md)]. The message that is sent to a bridge is a simple XML payload and has no headers. On the other hand, the outgoing message to the WCF service must have some SOAP headers defined. To [!INCLUDE[bridge](/Token/bridge_md.md)] this protocol mismatch, the persona that configures the [!INCLUDE[bridge](/Token/bridge_md.md)] uses the Route action to assign some relevant SOAP message headers, such as Action, MessageID, and so on to the outgoing message. After the [!INCLUDE[bridge](/Token/bridge_md.md)] is configured and deployed to the [!INCLUDE[sb2](/Token/sb2_md.md)], a POX message is sent to the [!INCLUDE[bridge](/Token/bridge_md.md)]. After processing the message but before routing the message to the WCF service, the headers specified in the Route action of the [!INCLUDE[bridge](/Token/bridge_md.md)] are stamped on the message and then sent to the WCF service, thus bridging the protocol mismatch.  To configure a Route action, see [The Routing Action](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_RoutingAction).

The following table lists how the property values can be transferred between intermediary stages (or the destination) of a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] using Route actions:

|From/To <br /> <br />|To other [!INCLUDE[bridge](/Token/bridge_md.md)]s <br /> <br />|To Queues and Topics <br /> <br />|To Relay or External Service Endpoints <br /> <br />|
|-----------|-----------------------------------------------------|------------------------|------------------------------------------|
|From [!INCLUDE[bridge](/Token/bridge_md.md)] <br /> <br />|The properties can’t be transferred as-is (key-value pairs) but can be passed on by assigning them as values of outgoing message headers (HTTP or SOAP) <br /> <br />|The properties can be transferred as-is (key-value pairs) and can also be passed on as values of outgoing message headers <br /> <br />|The properties can’t be transferred as-is (key-value pairs) but can be passed on by assigning them as values of outgoing message headers (HTTP or SOAP). However, it’s the prerogative of the bridge designer to ensure that relevant headers, which can be consumed by the relay or external service, are passed. <br /> <br />|

## <a name="BKMK_Send"></a>Reply Action
Reply action is exactly similar to Route action. The only difference is that while the Route action is applicable when the message is sent to the intended message receiver (either in [!INCLUDE[one-way](/Token/one-way_md.md)] or [!INCLUDE[request_response](/Token/request_response_md.md)]), the Reply action is applicable when the response message from a message receiver has to be routed back to the message sender (only in the case of [!INCLUDE[request_response](/Token/request_response_md.md)].)

To understand this better, you can simply reverse the scenario used for Route action. Consider that the message sender needs to send a SOAP message to REST service that expects POX/REST message, via an [!INCLUDE[request_response](/Token/request_response_md.md)]. The message that is sent to the [!INCLUDE[bridge](/Token/bridge_md.md)] is a SOAP message with all the relevant headers. The [!INCLUDE[bridge](/Token/bridge_md.md)], before routing the message to the REST service, implicitly strips the message headers and sends only the XML payload to the REST service. The response from the REST service is also a POX message. Before the POX response message is sent back to the message sender, the Reply action stamps the message headers on the POX message and then sends the SOAP enveloped message to the message sender. To configure a Reply action, see [Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Reply).

The following table lists how the property values can be transferred back from a [!INCLUDE[bridge](/Token/bridge_md.md)] to the message sending client using Reply actions:

|From/To <br /> <br />|To other [!INCLUDE[bridge](/Token/bridge_md.md)]s <br /> <br />|To Relay or External Service Endpoints <br /> <br />|
|-----------|-----------------------------------------------------|------------------------------------------|
|From [!INCLUDE[bridge](/Token/bridge_md.md)] <br /> <br />|The properties can’t be transferred as-is (key-value pairs) but can be passed on by assigning them as values of outgoing message headers (HTTP or SOAP) <br /> <br />|The properties can’t be transferred as-is (key-value pairs) but can be passed on by assigning them as values of outgoing message headers (HTTP or SOAP). However, it’s the prerogative of the bridge designer to ensure that relevant headers, which can be consumed by the relay or external service, are passed. <br /> <br />|

## Considerations While Setting the Header Properties through Route and Reply Actions
Even though you can use Route and Reply actions to set message header properties, you must consider the following points:

- You must be careful when using the **To** and **ReplyTo** SOAP message headers. This is because the underlying binding, such as WCF bindings, can override these message headers. So, if the application that consumes these messages is expecting the message headers that you set through Route or Reply actions, it might result in unexpected errors.

- You must not set the **MessageID** SOAP header when routing a message to endpoints that use **basicHttpBinding** or **basicHttpRelayBinding**.

## See Also
[What are Bridges?](/Topic/What_are_Bridges_.md)

