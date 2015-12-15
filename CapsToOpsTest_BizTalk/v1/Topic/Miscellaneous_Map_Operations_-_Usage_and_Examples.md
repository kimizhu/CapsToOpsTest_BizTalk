---
description: na
keywords: na
pagetitle: Miscellaneous Map Operations - Usage and Examples
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd6caf80-5425-41c1-a426-41071e5dba79
---
# Miscellaneous Map Operations - Usage and Examples

## Miscellaneous [!INCLUDE[mapop](/Token/mapop_md.md)]s
The following table lists the Misc [!INCLUDE[mapop](/Token/mapop_md.md)]s available [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]:

TABLE REMOVED

## Error and Data Handling
[!INCLUDE[af_integration](/Token/af_integration_md.md)] provides the ability to configure how an error is handled and how an empty or null node is handled. The error handling behavior of the following **Misc**[!INCLUDE[mapop](/Token/mapop_md.md)]s is configurable:

- **Get Context Property**

- **Number Format**

Steps:

1. Open a **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]** or the **BizTalk Service Artifacts** project in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)].

2. Double-click a [!INCLUDE[transform](/Token/transform_md.md)] (.trfm) to open the [!INCLUDE[transform](/Token/transform_md.md)] Designer.

3. In the [!INCLUDE[transform](/Token/transform_md.md)] toolbar, select **Settings**.

**Error Handling tab**

In the **Error Handling** tab, the following **Misc**[!INCLUDE[mapop](/Token/mapop_md.md)]s have two **Behavior** options:

- **Get Context Property**:

   - **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and the error is then sent to the client that sent the message.

   - **Output default value Null**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, Null is returned as the output.

- **Number Format**:

   - **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and the error is then sent back to the client that sent the message.

   - **Output default value Null**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, Null is returned as the output.

- **Any**:

   - **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and the error is then sent to the client that sent the message.

   - **Output default value Null**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, Null is returned as the output.

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

[Date &#47; Time Map Operations - Usage and Examples](/Topic/Date_/_Time_Map_Operations_-_Usage_and_Examples.md)

## See Also
[Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md)

