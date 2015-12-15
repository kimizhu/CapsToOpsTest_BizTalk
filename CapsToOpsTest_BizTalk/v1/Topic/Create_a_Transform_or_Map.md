---
description: na
keywords: na
pagetitle: Create a Transform or Map
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102686a-b1c5-467d-8f22-8fadec19189f
---
# Create a Transform or Map
You can define relationships between an input XML document, add [!INCLUDE[mapop](/Token/mapop_md.md)]s to modify the data, and then output an XML document. A [!INCLUDE[transform](/Token/transform_md.md)] or map is part of the [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK template in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)]. See [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md).

In this topic:

[Choose your Project type](/Topic/Create_a_Transform_or_Map.md#BKMK_ChooseProject)

[Add your Schemas](/Topic/Create_a_Transform_or_Map.md#BKMK_AddSchemas)

[Add your map operations](/Topic/Create_a_Transform_or_Map.md#BKMK_AddMaps)

[Design Area Tips and Tricks](/Topic/Create_a_Transform_or_Map.md#BKMK_DesignArea)

[More Map Stuff](/Topic/Create_a_Transform_or_Map.md#BKMK_More)

## <a name="BKMK_ChooseProject"></a>Choose your Project type
There are two ways to create a new [!INCLUDE[transform](/Token/transform_md.md)]: Add a map to the **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]** or create a new **BizTalk Service Artifacts** project.

When a map is added or created in the **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]**, it’s part of the project and is meant to be used in the [!INCLUDE[one-way](/Token/one-way_md.md)] or the [!INCLUDE[request_response](/Token/request_response_md.md)]. When you create a **BizTalk Service Artifacts** project, you are creating a map independent of any other project. When the [!INCLUDE[transform](/Token/transform_md.md)] is complete, it can be saved, added to a business to business agreement, or added to an existing [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

Many developers prefer to keep their schemas in a central location. In this situation, you can use **BizTalk Service Artifacts** project to store your schemas and your maps. Then, you save/backup one project and its resources. When you need those schemas or maps, you can simply add them to other projects.

#### Add a map to an existing BizTalk Services project

1. Open **[!INCLUDE[vsprvs](/Token/vsprvs_md.md)]** as Administrator and open your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

2. In the [!INCLUDE[af_integration](/Token/af_integration_md.md)] project, go to **Solution Explorer**.

3. Right-click the project, select **Add**, and select **New Item** or **Existing Item**.

4. Enter your map details and select **Add**.

After you’re done creating the map, you can add the map to the Transform Stage of the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]. See [Create an XML One-Way Bridge](/Topic/Create_an_XML_One-Way_Bridge.md) or [Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md). [Uses and Stages of Bridges](/Topic/Uses_and_Stages_of_Bridges.md) provides more information on the Transform Stage.

#### Create a new BizTalk Service Artifacts project

1. Open **[!INCLUDE[vsprvs](/Token/vsprvs_md.md)]** as Administrator.

2. Select **New Project**.

3. Expand the **[!INCLUDE[csprcs](/Token/csprcs_md.md)]** template and select **BizTalk Services**.

4. Select **BizTalk Service Artifacts**.

5. Enter the project **Name**, project **Location**, **Solution name** properties, and **Create directory for solution** preference.

6. Select **OK**.

When the project is opened, Map.trfm, Schema1.xsd, and Schema2.xsd are created automatically. These files are blank so you can change them, delete them, or add your own. [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[transform](/Token/transform_md.md)]s have a .trfm extension and opening a .trfm file opens the [!INCLUDE[transform](/Token/transform_md.md)] designer where you can add schemas, add [!INCLUDE[mapop](/Token/mapop_md.md)]s, and draw your links.

## <a name="BKMK_AddSchemas"></a>Add your Schemas
You can create and modify schemas using the built-in Schema Editor. After the map is added, add your Source schema (input) and Target schema (output):

1. Open a **[!INCLUDE[af_integration](/Token/af_integration_md.md)]** or **BizTalk Service Artifacts** project in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] as Administrator.

2. Add an existing schema (.xsd) or add a new schema (.xsd) to the project:

   1. Right-click the project and select **Add**.

   2. Select **Existing Item** to add a schema that is already created. Select **New Item**, **Schema** to create a new schema.

3. Select **Add**.

4. Double-click the schema (.xsd) to open the Schema Editor.

[Developing EDI Schemas](http://go.microsoft.com/fwlink/p/?LinkId=248181) provides information on creating and modifying existing schemas.

## <a name="BKMK_AddMaps"></a>Add your map operations
After the schemas are added, you can use the built-in [!INCLUDE[mapop](/Token/mapop_md.md)]s to change or manipulate the incoming data to match the output schema:

1. From the Toolbox, click and drag the [!INCLUDE[mapop](/Token/mapop_md.md)] to the [!INCLUDE[transform](/Token/transform_md.md)] designer:

   - [String Map Operations - Usage and Examples](/Topic/String_Map_Operations_-_Usage_and_Examples.md)

   - [Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md)

   - [Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md)

   - [List Map Operations - Usage and Examples](/Topic/List_Map_Operations_-_Usage_and_Examples.md)

   - [Cumulative Map Operations - Usage and Examples](/Topic/Cumulative_Map_Operations_-_Usage_and_Examples.md)

   - [Date &#47; Time Map Operations - Usage and Examples](/Topic/Date_/_Time_Map_Operations_-_Usage_and_Examples.md)

   - [Miscellaneous Map Operations - Usage and Examples](/Topic/Miscellaneous_Map_Operations_-_Usage_and_Examples.md)

   Double-click the [!INCLUDE[mapop](/Token/mapop_md.md)] to configure the inputs.

2. Click and drag items from  your input schema to the map operations or output schema to create the links. [!INCLUDE[mapop](/Token/mapop_md.md)]s support three input source types:

   - Link from a tree node

   - Link from a [!INCLUDE[mapop](/Token/mapop_md.md)]

   - Constant value

> [!TIP]
> - If a link from a tree node or a [!INCLUDE[mapop](/Token/mapop_md.md)] is not allowed, a message stating the reason is displayed in the Status Bar.
> - Some [!INCLUDE[mapop](/Token/mapop_md.md)]s have a **Type** property in the **Configure** dialog window. This **Type** property is read-only.

## <a name="BKMK_DesignArea"></a>Design Area Tips and Tricks

|||
|-|-|
|**Cut, Copy &amp; Paste** <br /> <br />|[!INCLUDE[mapop](/Token/mapop_md.md)]s are movable using Cut/Copy and Paste. Links are not movable using Cut/Copy and Paste. If you move a [!INCLUDE[mapop](/Token/mapop_md.md)] using Cut/Copy and Paste, the links are removed. <br /> <br />[!INCLUDE[mapop](/Token/mapop_md.md)]s and links cannot be dragged and dropped. To move [!INCLUDE[mapop](/Token/mapop_md.md)]s and their links, use **Ctrl + Click** to select the items to move. **Ctrl + Click** cuts the items and then you paste to the desired location. <br /> <br />|
|**XSLT Support** <br /> <br />|In a **[!INCLUDE[af_integration](/Token/af_integration_md.md)]** or **BizTalk Service Artifacts** project, a [!INCLUDE[transform](/Token/transform_md.md)] (.trfm) file can use XSLT. XSLT options include entering XSLT syntax and importing exiting XSLT files, including XML extension files (EXT XML). <br /> <br />To import an existing XSLT file, select the [!INCLUDE[transform](/Token/transform_md.md)] design area. In Properties, select **Import XSLT**. You can select a file or directly enter XSLT syntax. <br /> <br />To import an existing XML extension file, select the [!INCLUDE[transform](/Token/transform_md.md)] design area. In Properties, select **Import EXTXML**. You can select a file or directly enter XML syntax. <br /> <br />Select **Use XslCompiledTransform for better performance** to transform XML data by compiling XSLT style sheets and executing XSLT [!INCLUDE[transform](/Token/transform_md.md)]s. When the style sheet is compiled, it can be cached and reused. When this option is not enabled, the XslTransform class is used; which is best when a [!INCLUDE[transform](/Token/transform_md.md)] executes once. <br /> <br />|
|**Direct Links with Repeating Records** <br /> <br />|When linking a repeating record in the source document to a repeating record in the target document, a MapEach Loop is needed. Creating these links from each source node to the target node is often time consuming. As a result, [!INCLUDE[af_integration](/Token/af_integration_md.md)] includes Direct Link functionality. <br /> <br />Direct Linking is simply copying from an input node to an output node, with no other processing. Direct Linking is also used when linking non-repeating records; which does not require a MapEach Loop. <br /> <br />[Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md) describes the Direct Link functionality. <br /> <br />|
|**Scrolling** <br /> <br />|Scrolling vertically in the [!INCLUDE[transform](/Token/transform_md.md)] Designer can be done in two ways: <br /> <br /><ul><li>Scroll the mouse wheel </li><li>Using the Up and Down arrow keys </li> </ul>Scrolling horizontally in the [!INCLUDE[transform](/Token/transform_md.md)] Designer can be done in two ways: <br /> <br /><ul><li>Hold down the SHIFT key + scroll the mouse wheel </li><li>Using the Left and Right arrow keys </li> </ul>|
|**Drawing Surface** <br /> <br />|The drawing surface in the [!INCLUDE[transform](/Token/transform_md.md)] Designer has a default size of 200&#42;200 cells. To modify the size: <br /> <br /><ol><li>Go to the **Tools** menu and select **Options**. </li><li>Expand **[!INCLUDE[transform](/Token/transform_md.md)]s Designer** and click **General**. </li><li>Modify the **Number of Grid Cells on the X axis of the Grid Surface** and the **Number of Grid Cells on the Y axis of the Grid Surface** values. Values range from 100 to 1000. </li><li>Click **OK**. </li> </ol>|
|**Page** <br /> <br />|Pages can be added, deleted and renamed within the [!INCLUDE[transform](/Token/transform_md.md)] design surface. [!INCLUDE[mapop](/Token/mapop_md.md)]s and their scope containers are per page. <br /> <br />To add, remove, or rename a page, right-click the **Page 1** tab at the bottom of the design surface to view the available options. <br /> <br />|

## <a name="BKMK_More"></a>More Map Stuff
[Use standard XSD constructs in your maps](/Topic/Use_standard_XSD_constructs_in_your_maps.md)

[Transforms&#47;Maps Best Practices](/Topic/Transforms/Maps_Best_Practices.md)

[Loop and Scope Examples in map or transforms](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md)

## See Also
[Create Rich Messaging Endpoints on Azure](/Topic/Create_Rich_Messaging_Endpoints_on_Azure.md)
[Learn and create Message Maps and Transforms](/Topic/Learn_and_create_Message_Maps_and_Transforms.md)

