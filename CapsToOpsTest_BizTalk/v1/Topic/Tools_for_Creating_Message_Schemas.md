---
description: na
keywords: na
pagetitle: Tools for Creating Message Schemas
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70201659-05a5-44e2-9245-58f9a67345c9
---
# Tools for Creating Message Schemas
In the previous topics, we saw that rich messaging endpoints provide connectivity to different protocols and applications (see [Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md)), and provide message-processing capabilities such as validation, transformation, extraction, and enrichment on the cloud (see [What are Bridges?](/Topic/What_are_Bridges_.md)). However, neither of these can be used in isolation and ‘tie up’ with other [!INCLUDE[sb2](/Token/sb2_md.md)] entities on the cloud (like topics, queues, and so on) to provide an end-to-end message flow. For example, you could have a scenario where the a client sends a request message that needs to be processed on the cloud, routed to a queue, and then eventually inserted into a SQL Server database. To configure this scenario, you need to use an [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)], a [!INCLUDE[sb2](/Token/sb2_md.md)] queue, followed by [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] in a sequence. This presents a need for a design area where you could stitch different components of a message flow together. [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides a design surface called [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] that helps you achieve this. The [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface is available as a Visual Studio project type and is installed with [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK. For more information about the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and to set up a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], see [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

## Securing the BizTalk Service Project
In the current [!INCLUDE[sb2](/Token/sb2_md.md)] security model, access to the [!INCLUDE[sb2](/Token/sb2_md.md)] entities is controlled via [Access Control Service](http://go.microsoft.com/fwlink/p/?LinkId=225149) (http://go.microsoft.com/fwlink/p/?LinkId=225149). A valid [!INCLUDE[ac2](/Token/ac2_md.md)] token must be presented in order to create and manage entities on the [!INCLUDE[sb2](/Token/sb2_md.md)]. In most cases, a client sending a message to a [!INCLUDE[sb2](/Token/sb2_md.md)] entity must also present a valid [!INCLUDE[ac2](/Token/ac2_md.md)] token which is then used for authentication, the only known exception being relay endpoints that allow a client to be unauthenticated and handle the authentication and authorization on their own, typically using message security. Also, the [!INCLUDE[sb2](/Token/sb2_md.md)] does not propagate either the [!INCLUDE[ac2](/Token/ac2_md.md)] token or the claims received on the messages.

A [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] spanning multiple [!INCLUDE[sb2](/Token/sb2_md.md)] entities is a message-mediation intermediary that sits between the clients and the services. As such, a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] may be employed either by the service (in which case it mediates the receipt of messages sent by clients) or by a client (to mediate the messages before they are sent to service). In either case, effectively, the systems or applications employing the [!INCLUDE[sb2](/Token/sb2_md.md)] tend to be distributed with one of the parts being on the [!INCLUDE[sb2](/Token/sb2_md.md)] and others being outside the [!INCLUDE[sb2](/Token/sb2_md.md)], either on cloud or on premises. Hence, the distributed nature of these applications has implications on how authentication and authorization happens in various parts of the system in different scenarios.

For the current milestone, all the entities that are part of a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] must belong to the same [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. Hence, the authentication of a message flow happens only at the entry point of the flow and all entities in a message flow are considered to be within the same security and trust boundary. While deploying a message flow, you only need to provide the credentials (Issuer Name and Issuer Key) for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. For instructions on how to use a [!INCLUDE[msgflow](/Token/msgflow_md.md)] to configure rich messaging endpoints, see [Create the project in Visual Studio](/Topic/Create_the_project_in_Visual_Studio.md).

## Tools That Aid Application Development
[!INCLUDE[af_integration](/Token/af_integration_md.md)] provides the following tools that help in developing [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]s:

### Schema Editor
Schema Editor runs within the Microsoft Visual Studio environment. You can use it to easily create, edit, and manage XML and flat-file schemas for use with your application. Schema Editor uses its own graphical system of hierarchical records and fields to represent the structure of instance messages, and uses the XML Schema definition (XSD) language to store the schemas that it defines. This is true regardless of the format in which instance messages are exchanged: XML or flat-files.

**Creating Schemas Using the Schema Editor**

Working with Schema Editor is similar to working with Editor in BizTalk Server. To use the Schema Editor, you can use the steps at [Using BizTalk Editor](http://msdn.microsoft.com/library/aa559175%28v=bts.80%29.aspx).

> [!IMPORTANT]
> Unlike the BizTalk Server Editor, the [!INCLUDE[af_integration](/Token/af_integration_md.md)] Schema Editor does not enable you to generate an instance from a schema and test an instance against a schema.

**Testing Schemas Using the Schema Editor**

After you create your schema, you may want to validate that the schema describes the message structure you intend it to describe. Schema validation includes:

- Validating the schema

- Generating an instance of the schema

- Validating the instance against the schema

For more information on how to test the schema, see [http://msdn.microsoft.com/library/aa547850](http://msdn.microsoft.com/library/aa547850).

### Service Consuming Wizard
You can use bridges to send messages to external WCF service endpoints. If the incoming message to the bridge is of a schema different from the one expected by the external service endpoints, you must use transforms to map the incoming message schema to the message schema expected by the service. In turn, the transforms require that the schema of the message expected by the service be added to your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. To enable users to generate/add such schemas to the project, [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides the **Service Consuming Wizard**.

When you use the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] to route a message from a bridge to an external WCF service, you must have the schema of the service added to your project as well. The Service Consuming Wizard enables you to generate the schema of a WCF service and add it to your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. Once the schema is available as part of the project, you can use a transform to map the schema of the incoming message to the schema of the message expected by the service.

The **Service Consuming Wizard** in [!INCLUDE[af_integration](/Token/af_integration_md.md)] is similar to the BizTalk WCF Service Consuming Wizard in BizTalk Server. To use the wizard, you can use the steps at [Use the BizTalk WCF Service Consuming Wizard to Consume a WCF Service](http://msdn.microsoft.com/library/bb226552%28v=bts.80%29.aspx).

> [!NOTE]
> The only difference is that the [!INCLUDE[af_integration](/Token/af_integration_md.md)] wizard creates an XSD schema file after a successful run. The BizTalk Server wizard creates other output files that are not relevant for [!INCLUDE[af_integration](/Token/af_integration_md.md)].

## See Also
[BizTalk Services](/Topic/BizTalk_Services.md)

