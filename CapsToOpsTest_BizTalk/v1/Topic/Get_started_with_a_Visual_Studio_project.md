---
description: na
keywords: na
pagetitle: Get started with a Visual Studio project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03421690-817a-45a8-8492-c9cb98484102
---
# Get started with a Visual Studio project
The [!INCLUDE[msgflow](/Token/msgflow_md.md)] design area is a visual designer where you create an end-to-end message flow, originating from a message source, processed by a bridge, and then sent to a destination. It is a canvas that you can drag components onto from the Toolbox, and then use them to configure the flow.

When you install [!INCLUDE[af_integration](/Token/af_integration_md.md)], the installation adds the **BizTalk Services** category under the **Templates** area in the [!INCLUDE[vsprvs](/Token/vsprvs_md.md)]**New Project** dialog. The **BizTalk Services** category contains the following templates:

|Project Template <br /> <br />|Description <br /> <br />|
|--------------------|---------------|
|**BizTalk Service** <br /> <br />|Use this template to create a new [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] for creating [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications consisting of message sources, bridges, and message destinations. This project type is also used to create artifacts like schemas and transforms that are used by the [!INCLUDE[af_integration](/Token/af_integration_md.md)] application. <br /> <br />|
|**BizTalk Service Artifacts** <br /> <br />|Use this template to create a project that contains only the artifacts, namely [!INCLUDE[transform](/Token/transform_md.md)]s and Schemas. You can use this project to create a [!INCLUDE[transform](/Token/transform_md.md)] or a schema that you want to upload to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] for creating your agreements. <br /> <br />|
In this topic:

[Create a BizTalk Services Project](/Topic/Get_started_with_a_Visual_Studio_project.md#BKMK_CreateProject)

[Add Components to a BizTalk Services Project](/Topic/Get_started_with_a_Visual_Studio_project.md#BKMK_Components)

[Add Schemas and Transforms to your Project](/Topic/Get_started_with_a_Visual_Studio_project.md#BKMK_AddItems)

## <a name="BKMK_CreateProject"></a>Create a BizTalk Services Project
To create rich messaging endpoints, you need to start by creating a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]:

1. Open [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] as an administrator. On the **File** menu, select **New**, and then select **Project**.

2. In **New Project**, in the **Installed Templates** area, select **BizTalk Services**.

3. From the right-hand pane, select the **BizTalk Service** or **BizTalk Service Artifacts** template.

4. Enter the project name, location, and the name of the solution this project is a part of. If you want this solution to have a separate folder in Windows Explorer, select **Create directory for solution**.

5. Select **OK**.

> [!CAUTION]
> When you create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], it adds a MessageFlowitinerary.bcs file to the project. You should never delete the .bcs file from a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] because you can’t add a standalone .bcs file to an existing project. If you delete the .bcs file, create a new [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], and copy over the artifacts (schemas and [!INCLUDE[transform](/Token/transform_md.md)]s) from the old project to the new one.

**To add a  [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] to an existing solution**

1. Open [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] as an administrator. Open an existing solution in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], right-click the solution name, select **Add**, and then select **New Project**.

2. In **Add New Project**, in the **Installed Templates** area, select **BizTalk Services**.

3. From the right-hand pane, select the **BizTalk Service** or **BizTalk Service Artifacts** template.

4. Enter the name and location of the project.

5. Select **OK**.

## <a name="BKMK_Components"></a>Add Components to a BizTalk Services Project
[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] designer provides several components that you can place on the design area as visual representations of the message sources, message processing bridges, or message destinations. These components can help you to efficiently design and implement a message flow.

**To add a component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]**, drag the component from the toolbox to the design area. To remove a component, right-click the component, and select **Delete**.

The following table lists the available components, along with a brief description of the function of each shape:

|Name <br /> <br />|Purpose <br /> <br />|More Information <br /> <br />|
|--------|-----------|--------------------|
|Connector <br /> <br />|Connects two components in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and routes the messages from one component to another. <br /> <br />|[Routing Messages from Bridges to Destinations in the BizTalk Service Project](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md) <br /> <br />|
**BRIDGES**

||||
|-|-|-|
|[!INCLUDE[one-way](/Token/one-way_md.md)] <br /> <br />|A one-way [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] that processes a request message from a client that does not expect a response. <br /> <br />|[Create an XML One-Way Bridge](/Topic/Create_an_XML_One-Way_Bridge.md) <br /> <br />|
|[!INCLUDE[request_response](/Token/request_response_md.md)] <br /> <br />|A two-way, request-reply [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] that processes a request message from a client that expects a response. <br /> <br />|[Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md) <br /> <br />|
|[!INCLUDE[passthru](/Token/passthru_md.md)] <br /> <br />|A pass-through bridge that passes the input message to the destination entity, as-is. <br /> <br />|[Create a Pass-Through Bridge](/Topic/Create_a_Pass-Through_Bridge.md) <br /> <br />|
**DESTINATIONS**

||||
|-|-|-|
|Azure Blob Destination <br /> <br />|Routes a message to an Azure Blob. <br /> <br />|[Configure an Azure Blob Destination](/Topic/Configure_an_Azure_Blob_Destination.md) <br /> <br />|
|FTP Destination <br /> <br />|Routes a message to a folder on an FTP Server. <br /> <br />|[Configure an FTP Destination](/Topic/Configure_an_FTP_Destination.md) <br /> <br />|
|One-Way External Service Endpoint <br /> <br />|Routes a message to a one-way external service that takes a request but does not return anything in response. <br /> <br />|[Include a One-Way External Service Endpoint](/Topic/Include_a_One-Way_External_Service_Endpoint.md) <br /> <br />|
|One-Way Relay Endpoint <br /> <br />|Routes a message to a one-way relay endpoint (on [!INCLUDE[sb2](/Token/sb2_md.md)]) that takes a request but does not return anything in response. <br /> <br />|[Include a One-Way Relay Endpoint](/Topic/Include_a_One-Way_Relay_Endpoint.md) <br /> <br />|
|[!INCLUDE[sb2](/Token/sb2_md.md)] Queue Destination <br /> <br />|Routes a message to a [!INCLUDE[sb2](/Token/sb2_md.md)] queue. <br /> <br />|[Include a Service Bus Queue Destination](/Topic/Include_a_Service_Bus_Queue_Destination.md) <br /> <br />|
|SFTP Destination <br /> <br />|Routes a message to a folder on an SFTP Server. <br /> <br />|[Configure an SFTP Destination](/Topic/Configure_an_SFTP_Destination.md) <br /> <br />|
|[!INCLUDE[sb2](/Token/sb2_md.md)] Topic Destination <br /> <br />|Routes a message to a [!INCLUDE[sb2](/Token/sb2_md.md)] topic. <br /> <br />|[Include a Service Bus Topic Destination](/Topic/Include_a_Service_Bus_Topic_Destination.md) <br /> <br />|
|Two-Way External Service Endpoint <br /> <br />|Routes a message to a two-way external service that takes a request and gives back a response. <br /> <br />|[Include a Two-Way External Service Endpoint](/Topic/Include_a_Two-Way_External_Service_Endpoint.md) <br /> <br />|
|Two-Way Relay Endpoint <br /> <br />|Routes a message to a two-way relay endpoint (on [!INCLUDE[sb2](/Token/sb2_md.md)]) that takes a request and gives back a response. <br /> <br />|[Include a Two-Way Relay Endpoint](/Topic/Include_a_Two-Way_Relay_Endpoint.md) <br /> <br />|
**SOURCES**

||||
|-|-|-|
|FTP Source <br /> <br />|Receives a message from a folder on an FTP Server. <br /> <br />|[Add a Message Source to the Bridge](/Topic/Add_a_Message_Source_to_the_Bridge.md) <br /> <br />|
|[!INCLUDE[sb2](/Token/sb2_md.md)] Queue Source <br /> <br />|Receives a message from a [!INCLUDE[sb2](/Token/sb2_md.md)] Queue. <br /> <br />|[Add a Message Source to the Bridge](/Topic/Add_a_Message_Source_to_the_Bridge.md) <br /> <br />|
|SFTP Source <br /> <br />|Receives a message from a folder on an SFTP Server. <br /> <br />|[Add a Message Source to the Bridge](/Topic/Add_a_Message_Source_to_the_Bridge.md) <br /> <br />|
|[!INCLUDE[sb2](/Token/sb2_md.md)] Subscription Source <br /> <br />|Receives messages from a [!INCLUDE[sb2](/Token/sb2_md.md)] Topic subscription. <br /> <br />|[Add a Message Source to the Bridge](/Topic/Add_a_Message_Source_to_the_Bridge.md) <br /> <br />|

## <a name="BKMK_AddItems"></a>Add Schemas and Transforms to your Project
A **schema** is the definition of the structure for a document or message. It contains property information as it pertains to the records and fields within the structure. If appropriate, a schema can contain multiple subschemas. In a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], you can add either an XML schema or a flat-file schema.

A **[!INCLUDE[transform](/Token/transform_md.md)]** is an XML file that defines the correspondence between the records and fields in one schema and the records and fields in another schema. You create [!INCLUDE[transform](/Token/transform_md.md)]s based on industry standards, non-industry standards (such as internal standards or legacy issues), or existing files. You create [!INCLUDE[transform](/Token/transform_md.md)]s when you want to map data that you receive or send from one format to another. You can use the [!INCLUDE[transform](/Token/transform_md.md)] project item to create maps that you include in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. All [!INCLUDE[transform](/Token/transform_md.md)]s that you save have a **.trfm** file extension. For more information about [!INCLUDE[transform](/Token/transform_md.md)]s, see [Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md).

#### To add a new schema or transform to a BizTalk Service project

1. In a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], right-click the project name, select **Add**, and then select **New Item**.

2. In the **Add New Item** dialog box, select **Schema**, **Flat File Schema**, or **Map**.

   > [!NOTE]
   > You can also create a flat-file schema from scratch or create a flat-file schema using a flat-file instance message. Select **Generate Flat File Schema** to open the **Flat File Schema Wizard**. To use the wizard, see [How to Use the Flat File Schema Wizard](/Topic/How_to_Use_the_Flat_File_Schema_Wizard.md).

3. Enter a name and then select **OK**.

## See Also
[Create the project in Visual Studio](/Topic/Create_the_project_in_Visual_Studio.md)

