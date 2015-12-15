---
description: na
keywords: na
pagetitle: Date / Time Map Operations - Usage and Examples
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d52e64e7-120b-4186-828e-4a35cfcd5131
---
# Date / Time Map Operations - Usage and Examples
Lists the Date/Time [!INCLUDE[mapop](/Token/mapop_md.md)]s in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)].

## Date/Time [!INCLUDE[mapop](/Token/mapop_md.md)]s

|[!INCLUDE[mapop](/Token/mapop_md.md)] <br /> <br />|Description <br /> <br />|Parameters <br /> <br />|Output <br /> <br />|
|-----------------------------------------|---------------|--------------|----------|
|DateTime Reformat <br /> <br />|Reformats a date/time value. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input* <br /> <br />A link from a tree node. <br /> <br />In **Input Format**, specify the appropriate format. In **Output Format**, specify the desired output format. <br /> <br />|The incoming date/time value will be formatted to the new output format. <br /> <br />|
|Generate Date Time <br /> <br />|Generates the current Date/Time. <br /> <br />|In **Output Format**, specify the desired format. <br /> <br />|The incoming value is generated using the Date/Time format specified. <br /> <br />|
|Adjust TimeZone <br /> <br />|Converts a date/time value to a different time zone. An Input Date is parsed and then converted from the Input time zone to the Output time zone. <br /> <br />Some key points: <br /> <br /><ul><li>When only a date is specified for **Input Date**, 12AM is used for the time. </li><li>When the Input Date value contains the "K" format, the **Input TimeZone** option is grayed out. At runtime, the Input Time Zone is extracted from the Input Date value. If Input Date is not present, UTC is used. </li> </ul>|Requires exactly one input parameter: <br /> <br />*Input Date* <br /> <br />A link from a tree node or an entered date value. <br /> <br />Also specify the following: <br /> <br /><ul><li>**Input Format**: Select a Date/Time format of the Input Date specified. </li><li>**Input TimeZone**: </li><li>**Output TimeZone**: </li> </ul>|The incoming Date value is converted to the Output time zone. <br /> <br />|

### Known Issue
When a DateTime Reformat [!INCLUDE[mapop](/Token/mapop_md.md)] is added to the design area and configured, the **Format** drop-down list may be grayed out. This can happen if the computer Display is set **Medium – 125%** or **Larger – 150%**.

To resolve, set the display to **Smaller – 100% (default)** using the following steps:

1. Open the **Control Panel** and select **Appearance and Personalization**.

2. Select **Display**.

3. Select **Smaller – 100% (default)** and select **Apply**.

The Format drop-down list should now work as expected.

## Error and Data Handling
[!INCLUDE[af_integration](/Token/af_integration_md.md)] provides the ability to configure how an error is handled and how an empty or null node is handled. The error handling behavior of **Date / Time** is configurable in a **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]** and the **BizTalk Service Artifacts** project. Steps:

1. Open a **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]** or a **BizTalk Service Artifacts** project in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)].

2. Double-click a [!INCLUDE[transform](/Token/transform_md.md)] (.trfm) to open the [!INCLUDE[transform](/Token/transform_md.md)] Designer.

3. In the [!INCLUDE[transform](/Token/transform_md.md)] toolbar, select **Settings**.

**Error Handling tab**

In the **Error Handling** tab, **Date / Time Operations** have two **Behavior** options:

- **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and is then sent to the user who sent the message.

- **Output default value Null**: A null value is returned as the output. A null value behaves as an empty value behaves *except* when sorting a List. When sorting a List, null values are considered less than empty values.

**Null/Empty Data Handling tab**

In the **Null/Empty Data Handling** tab, there are three options:

- **Consider empty nodes in cumulative operations**: By default, this is not checked. When not checked, no empty nodes are included in the iteration. When checked, all nodes, including empty nodes, are included in the iteration.

   EXAMPLE: There is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. When **Consider empty nodes in iterations** is not checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] returns a value of seven. When **Consider empty nodes in iterations** is checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] returns a value of 10.

- **Consider empty nodes in iterations**: By default, this is not checked. When not checked, no empty nodes are included in the iteration. When checked, all nodes, including empty nodes, are included in the iteration.

   EXAMPLE: there is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. When **Consider empty nodes in iterations** is not checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] iterates seven times for the non-empty nodes. As a result, seven &lt;record&gt; nodes are generated in the Target. When **Consider empty nodes in iterations** is checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] iterates 10 times for all nodes, including the empty nodes. As a result, 10 &lt;record&gt; nodes are generated in the Target.

- **Target Node Generation**: If empty nodes are configured to be considered, you choose to generate an empty node in the output or to not generate an empty node in the output. Specifically:

   - Do not generate empty nodes: Default option.

   - Generate empty nodes

   EXAMPLE: There is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. **Consider empty nodes in cumulative operations** or **Consider empty nodes in iterations** are not checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] iterates seven times for the non-empty nodes. As a result, seven &lt;record&gt; nodes are generated in the Target. When **Consider empty nodes in iterations** is checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] iterates 10 times for all nodes, including the empty nodes. As a result, 10 &lt;record&gt; nodes are generated in the Target.

## Additional [!INCLUDE[mapop](/Token/mapop_md.md)]s
[String Map Operations - Usage and Examples](/Topic/String_Map_Operations_-_Usage_and_Examples.md)

[Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md)

[Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md)

[List Map Operations - Usage and Examples](/Topic/List_Map_Operations_-_Usage_and_Examples.md)

[Cumulative Map Operations - Usage and Examples](/Topic/Cumulative_Map_Operations_-_Usage_and_Examples.md)

[Miscellaneous Map Operations - Usage and Examples](/Topic/Miscellaneous_Map_Operations_-_Usage_and_Examples.md)

## See Also
[Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md)

