---
description: na
keywords: na
pagetitle: Flat-file Support In One-Way Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e4242c5-9230-4960-b72f-a679834197c6
---
# Flat-file Support In One-Way Bridge
Flat file message transfer is a key requirement in [!INCLUDE[af_integration](/Token/af_integration_md.md)] scenarios. Many enterprise applications receive flat file messages from client applications, such as SAP IDOCs. To enable flat-file processing over the cloud, you can use [!INCLUDE[bridge](/Token/bridge_md.md)]s available as part of [!INCLUDE[af_integration](/Token/af_integration_md.md)] .

## Flat File Support: What’s In and What’s Not?
The following table lists the flat-file processing features available with [!INCLUDE[af_integration](/Token/af_integration_md.md)]:

|What’s In <br /> <br />|What’s Not <br /> <br />|
|-------------|--------------|
|**Receive flat-file messages**. You can configure a [!INCLUDE[bridge](/Token/bridge_md.md)] to receive flat-file messages either over HTTP or FTP. <br /> <br />|**Support for [!INCLUDE[request_response](/Token/request_response_md.md)]**. You cannot configure an [!INCLUDE[request_response](/Token/request_response_md.md)] to process flat file messages. You cannot have an [!INCLUDE[request_response](/Token/request_response_md.md)] sending flat file messages to the message receiving entity or back to the client that sent the original flat file message. <br /> <br />|
|**Sending out flat-file messages**. You can configure a [!INCLUDE[bridge](/Token/bridge_md.md)] to send out flat-file messages, which makes the following scenarios possible: <br /> <br /><ul><li>*Flat file in, Flat file out* </li><li>*Flat file in, XML out* </li><li>*XML in, Flat file out* </li><li>*XML in, XML out* </li> </ul>||
|**Support for [!INCLUDE[one-way](/Token/one-way_md.md)]**. You can configure a [!INCLUDE[one-way](/Token/one-way_md.md)] to receive and send flat-file messages. <br /> <br />||
|**Support for receiving messages of different flat-file schemas using the same bridge**. You can configure a [!INCLUDE[one-way](/Token/one-way_md.md)] bridge to receive flat-file messages of more than one schema. <br /> <br />||
|**Support for receiving flat-file and XML messages using the same bridge**. You can configure the same [!INCLUDE[one-way](/Token/one-way_md.md)] to receive both flat-file messages as well as XML messages. <br /> <br />||

## How Does an [!INCLUDE[one-way](/Token/one-way_md.md)] Handle Flat File Messages?
With the flat-file support, an [!INCLUDE[one-way](/Token/one-way_md.md)] can process both flat-file and XML messages at the same endpoint. So, you don’t need to configure and deploy two separate [!INCLUDE[bridge](/Token/bridge_md.md)]s on the [!INCLUDE[sb2](/Token/sb2_md.md)] to process different message types; a single [!INCLUDE[bridge](/Token/bridge_md.md)] does both for you.

### Receiving Flat-file Messages
While receiving a message, the [!INCLUDE[bridge](/Token/bridge_md.md)] detects the message format (flat file or XML) based on the **&#42;content-type&#42;** HTTP header. This header is mandatory for all incoming messages to be processed by the [!INCLUDE[bridge](/Token/bridge_md.md)]. If the header is not present, it results in a runtime error. If the message is coming over HTTP, the content-type is set by default. If the message is coming over FTP, this header is set by the FTP source entity that posts data to the [!INCLUDE[bridge](/Token/bridge_md.md)] endpoint.

> [!NOTE]
> You can configure an FTP source entity on the [!INCLUDE[msgflow](/Token/msgflow_md.md)] surface that defines the FTP location from where the message is picked. For more information, see [Add a Message Source to the Bridge](/Topic/Add_a_Message_Source_to_the_Bridge.md).

Bridges support the following message types:

- Application/xml

- Application/soap+xml

- Text/xml

- Text/plain

Of these, the content-type “text/plain” maps to flat file messages. To process text/plain messages, a [!INCLUDE[bridge](/Token/bridge_md.md)] includes a ‘Decode’ stage that is the first stage in the [!INCLUDE[bridge](/Token/bridge_md.md)] before the Validate, Enrich, Transform, and Enrich (post-Transform) stages.

- If a [!INCLUDE[bridge](/Token/bridge_md.md)] receives a message of ‘text/plain’ content type, the decode stage decodes the message and converts it to an XML message. Rest of the processing at each stage within the [!INCLUDE[bridge](/Token/bridge_md.md)] happens on the XML message and not the flat file message.

- If a message with the any of the other content types is received by the [!INCLUDE[bridge](/Token/bridge_md.md)], the decode stage is not activated and no flat-file decoding happens. The incoming message is then passed over to the other stages, where it is processed based on the stage configuration.

### Sending Out Flat-file Messages
While sending out messages from a [!INCLUDE[bridge](/Token/bridge_md.md)], you can configure a [!INCLUDE[bridge](/Token/bridge_md.md)] to send out flat-file messages using the **Flat File Encode** activity within the **Encode** stage. If you enable the stage, the [!INCLUDE[bridge](/Token/bridge_md.md)] can send out flat-file messages and XML messages. If you disable the stage, the [!INCLUDE[bridge](/Token/bridge_md.md)] only sends out XML messages. As mentioned earlier, even if a flat-file message is received by the [!INCLUDE[bridge](/Token/bridge_md.md)], it gets converted to XML message at the decode stage and is then processed as an XML message by the other stages of a [!INCLUDE[bridge](/Token/bridge_md.md)]. Once the XML message reaches the **Encode** stage, the message type of the XML message is matched with the schema specified as part of the **Flat File Encode** activity. If a match occurs, the schema is used to convert the XML message to a flat-file message. The content-type for such messages is set to “text/plain”. If no match is found, the XML message is sent out of the [!INCLUDE[bridge](/Token/bridge_md.md)] as-is. For more information, see [Create an XML Bridge](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_Encode).

## Processing Multiple Flat Files Using a Single [!INCLUDE[one-way](/Token/one-way_md.md)]
For XML messages, [!INCLUDE[bridge](/Token/bridge_md.md)]s support processing messages of more than one message type using the same [!INCLUDE[bridge](/Token/bridge_md.md)] endpoint. They do so by identifying a message using the message type, which is a combination of the target namespace and the schema root node name, for example `http://IntegrationServices.Schema#RootNode`. The same cannot be true for flat file messages because there is no target namespace. So, to provide the ability to process flat-file messages of more than one type at the same [!INCLUDE[bridge](/Token/bridge_md.md)] endpoint, [!INCLUDE[bridge](/Token/bridge_md.md)]s use the concept of ‘tags’. Following are some considerations with respect to tags:

- All flat-file schemas should have tags defined as part of schema definition.

- At most, there can be only one flat-file schema that does not have an associated tag with it. If you add more than one untagged schema, it results in a build error.

When a flat-file message is received by the [!INCLUDE[bridge](/Token/bridge_md.md)], it matches the tag in the incoming message with the tags in all the flat-file schemas, in the order in which they were added to the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration. If a match happens, that schema is used to validate the incoming message. The only exception to this rule is that if there is one schema without a tag, it is evaluated at the end.

> [!IMPORTANT]
> You can have schemas that have tags defined both at the root level as well as the child record level. For schema validation, only the tags at the root level are considered.

## More Information about Flat File Messages
For more information on flat-file messages, refer to [Structure of a Flat File Message](http://go.microsoft.com/fwlink/?LinkId=245793).

## In This Section

- [How to Use the Flat File Schema Wizard](/Topic/How_to_Use_the_Flat_File_Schema_Wizard.md)

## See Also
[Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md)

