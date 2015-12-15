---
description: na
keywords: na
pagetitle: Uses and Stages of Bridges
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e49765d-97e5-407e-9d9c-698060c0249e
---
# Uses and Stages of Bridges
[!INCLUDE[af_integration](/Token/af_integration_md.md)] provides two kinds of bridges – [!INCLUDE[passthru](/Token/passthru_md.md)] and [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]. [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]s, in turn include [!INCLUDE[one-way](/Token/one-way_md.md)] and [!INCLUDE[request_response](/Token/request_response_md.md)]. This section provides information on the uses and stages of these [!INCLUDE[bridge](/Token/bridge_md.md)]s.

## XML Bridges

### Uses of an XML Bridge
The [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] can be used to mediate and bridge mismatches between two or more disparate systems that communicate by exchanging XML messages. [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]s, possibly in conjunction with other [!INCLUDE[sb2](/Token/sb2_md.md)] entities in a message flow, provide a variety of mediation paradigms and scenarios, such as following:

- **Message Validation**: The [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] supports validation of incoming XML messages against an XSD schema. Messages that fail validation are rejected.

- **Message Enrichment and Extraction**: The [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] supports message enrichment through data lookup from other data sources. This is typically useful in scenarios where messages may require contextual data present beyond the message boundaries typically from a configuration store, an external service, or the likes.

   The [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] also enables you to extract properties from an XML message that can be used for routing eventually. For example, in a purchase order message, the **Quantity** element can be marked. The message can then be routed based on the value of quantity ordered.

- **Message Transformation**: The [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] supports message body transformations from one XML structure to another. This capability of an [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] can also be used to ‘normalize’ a message in scenarios where multiple messages are mapped to a single message. For example, a [!INCLUDE[bridge](/Token/bridge_md.md)] may need to accept purchase orders in different schemas from different clients but they are eventually transformed into a single purchase order schema required by the organization.

- **Location Virtualization**: The [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] provides primitive location virtualization of backend services. Clients send messages to the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] endpoint exposed on the cloud and not the actual service (which may be on the cloud or on premises). The bridge then routes the messages to the backend service based on routing rules.

- **Custom processing**: The [!INCLUDE[bridge](/Token/bridge_md.md)]s provide the options of including custom code to incorporate processing tasks that are not included in the out-of-the-box [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

### <a name="BKMK_Stage"></a>Stages of an XML Bridge
This section provides information about the different stages of an [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]. Note that each stage is optional and can be turned *on* or *off*.

#### <a name="BKMK_Validate"></a>Validate Stage
The first stage in the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] is the **Validate** stage. This provides XSD validation of XML messages against specified schemas. The schemas to use for validation are specified during the configuration of the [!INCLUDE[bridge](/Token/bridge_md.md)]. A single [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] can receive and process XML messages with different schemas. During the validate stage, depending on the incoming message, the corresponding schema is picked and used for validation. Once the message is validated against the schema, the **Validate** stage promotes the **X_PIPELINE_MESSAGETYPE** property on the message. The value of the property is a combination of target namespace for the schema and the root node name, for example, `http://IntegrationServices.Schema#RootNode`. If the message validation fails either because no matching schema was found or because of an ambiguous match (more than one schema matched), an exception is thrown.

For instructions on how to configure the validate stage, see [Create an XML One-Way Bridge](/Topic/Create_an_XML_One-Way_Bridge.md) or [Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md).

#### <a name="BKMK_Extract"></a>Enrich Stage
Within the **Enrich** stage you can enrich a message by creating properties, the values of which can be derived from the incoming message header, from a system-promoted property, from an element or attribute in the incoming message body, or through a lookup on an external data source such as [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] tables. These properties can then be used for routing messages to destination endpoints and protocol bridging.

TABLE REMOVED

While the information about the providers is stored in the LookupProviderConfigurations.xml, the information about which values to assign from header to message properties, what values to extract, and what values to lookup are stored in a bridge configuration file. When you build a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], the LookupProviderConfigurations.xml also rolls up into a bridge configuration file. When you deploy the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], it is this bridge configuration file that gets deployed to the [!INCLUDE[sb2](/Token/sb2_md.md)].

##### What Can I do with the Properties?
In the Enrich stage, you create properties and assign values to those properties. But the question that comes to mind is what can I do with these properties? How do these properties make my task easier? You can use the properties in two ways:

- You can use the properties to set filter conditions to route messages to different destinations. For instructions on how to achieve this, see [The Routing Condition](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_Filter).

- You can use the properties to bridge protocol mismatch between the message sender and the message receiver. For example, you have an incoming SOAP message that has a custom header value. You want to pass on this value as the custom header of an HTTP message because the message receiver wants a REST message and does not understand a SOAP message format. You can use properties to do so. You can first assign the value from the incoming message header to a property, say P1, and then while sending the message to the receiver, assign the value of P1 to the message header of the outgoing message. For more information, see [Route and Reply Actions: Bridging Protocol Mismatch](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md) .

##### What is the Lifetime of the Properties?
Within a [!INCLUDE[msgflow](/Token/msgflow_md.md)], the properties that you define as part of the Enrich stage are available throughout the flow of the message for each stage in [!INCLUDE[msgflow](/Token/msgflow_md.md)]. In other words, if you defined a property in the Enrich stage, you can use that property during the Transform stage as well as for any map operations. The properties defined in the Enrich stage can also be used outside the boundary of a [!INCLUDE[msgflow](/Token/msgflow_md.md)], with some considerations. Before we go into the details of that, we must understand that the property values are stored as properties of the [!INCLUDE[sb2](/Token/sb2_md.md)][BrokeredMessage](http://go.microsoft.com/fwlink/p/?LinkId=227144) class. Now that we are aware of this fact, let’s talk about the lifetime of the properties outside a [!INCLUDE[msgflow](/Token/msgflow_md.md)].

- Because only a [!INCLUDE[sb2](/Token/sb2_md.md)] Queue or a Topic can consume messages of BrokeredMessage type, the properties and their values (as a key-value pair), can directly be consumed by Queues and Topics. After that, Topics for instance, can potentially use the properties for further processing and routing

- You cannot pass on the properties and their values to other [!INCLUDE[msgflow](/Token/msgflow_md.md)] components like One-Way/Two-Way Relay Endpoints or One-Way/Two-Way External Service Endpoints. If you do want to pass the property values to these entities, you must assign the property values to the headers of the outgoing message. For more information, see [Route and Reply Actions: Bridging Protocol Mismatch](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md).

- In a “chaining” scenario where the message from one [!INCLUDE[bridge](/Token/bridge_md.md)] is routed to another [!INCLUDE[bridge](/Token/bridge_md.md)] and then finally to a [!INCLUDE[sb2](/Token/sb2_md.md)] Queue (for example), only the properties from the last bridge in the chain are available for any further routing or processing. Also, to pass property values to the subsequent bridges, property values must be assigned to the headers of the outgoing message. These properties must then be extracted in the second bridge.

#### <a name="BKMK_Transform"></a>Transform Stage
The **Transform** stage, as the name suggests, provides the capability to perform structural transformations on the messages. Like the other stages in the pipeline, the **Transform** stage can work with multiple message-types, so you can have more than one transform available as part of the transform stage. The right transform to be performed is automatically looked up at runtime based on the incoming message type, provided the corresponding transforms have been configured and uploaded while configuring the bridge. The transform resolution happens based on the message type of the incoming message.

- The Transform stage matches the message type of the message with the message type of the source schema in a map.

- If the validation stage is turned off, the transform stage matches the incoming message with the source message schema. If the resolution happens, it then promotes the **MessageType** property on the message.

The current release only supports single source to single destination transforms. For more information, see [Learn and create Message Maps and Transforms](/Topic/Learn_and_create_Message_Maps_and_Transforms.md). For instructions on how to configure the Transform stage, see [Create an XML Bridge](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_Transform) or [XML Request-Reply Bridge : Configuring the Enrich Stage for the Response Message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Transform).

#### <a name="BKMK_ExtractPT"></a>Enrich Stage – Post Transform
The **Enrich** stage, post transform, is similar to the Enrich stage before transform. The only difference is that in the post-transform Enrich stage, you can enrich the transformed message. The way you configure the Enrich stage remains the same as pre-transform Enrich stage.  For instructions on how to configure the Enrich stage, post transform see [Create an XML Bridge](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_EnrichPostTrans) or [XML Request-Reply Bridge : Configuring the Enrich Stage for the Response Message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_EnrichPostTrans).

> [!NOTE]
> All the properties extracted or looked up before the transform stages are also available on the transformed message. A previously extracted or enriched property will be overwritten if it is modified in the post-transform enrich stage.

### <a name="BKMK_artifact"></a>Artifacts for an XML Bridge
In the previous section we saw that in the **Validate** stage, the validation happens against schemas and in the **Transform** stage, the message is transformed using a transform. So, the artifacts those are available as part of an [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] are:

- **Schemas**. These have .XSD extension

- **Transforms**. These have .TRFM extension and there can be multiple transforms within a Transform stage.

- **Assemblies**. These include the custom-processing logic that can be incorporated at specific stages of the bridge.

- **Certificates**. These are used for secure message transfer.

> [!NOTE]
> A bridge configuration file is not an artifact because it cannot be shared between different bridges. A bridge configuration file is specific to a bridge.

The BizTalk Service application can have multiple [!INCLUDE[bridge](/Token/bridge_md.md)]s and each [!INCLUDE[bridge](/Token/bridge_md.md)] can be using multiple transforms and schemas. So, a typical [!INCLUDE[af_integration](/Token/af_integration_md.md)] application would have a large number of transforms and schemas. However, at the same time, every transform and schema might not be required for each [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]. Hence, there must be a way to associate the transforms and schemas to a bridge. You can do this association while configuring the bridge.

To associate schemas and transforms, see [Create an XML One-Way Bridge](/Topic/Create_an_XML_One-Way_Bridge.md) or [Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md).

## Pass-Through Bridges
A [!INCLUDE[passthru](/Token/passthru_md.md)] is used when you want any message type to be processed by the bridge. As a result, a [!INCLUDE[passthru](/Token/passthru_md.md)] does not include validate or transform stages because both these stages are tied to message types. A [!INCLUDE[passthru](/Token/passthru_md.md)] only includes the **Enrich** stage, which is used for the same purposes as in an [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]. For more information on how to configure a [!INCLUDE[passthru](/Token/passthru_md.md)], see [Create a Pass-Through Bridge](/Topic/Create_a_Pass-Through_Bridge.md).

## See Also
[What are Bridges?](/Topic/What_are_Bridges_.md)

