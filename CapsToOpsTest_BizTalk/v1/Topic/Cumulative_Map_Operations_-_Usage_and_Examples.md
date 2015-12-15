---
description: na
keywords: na
pagetitle: Cumulative Map Operations - Usage and Examples
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 20c93d81-5f15-4545-8f60-24fa5479870d
---
# Cumulative Map Operations - Usage and Examples
Lists the Cumulative [!INCLUDE[mapop](/Token/mapop_md.md)]s in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)].

## Cumulative [!INCLUDE[mapop](/Token/mapop_md.md)]s

|[!INCLUDE[mapop](/Token/mapop_md.md)] <br /> <br />|Description <br /> <br />|Parameters <br /> <br />|Output <br /> <br />|
|-----------------------------------------|---------------|--------------|----------|
|Cumulative Sum <br /> <br />|Returns the accumulated value of a record. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input:* <br /> <br />A link from a tree node or a List operation that contains a numeric value. When using a List, the Cumulative operation can operate on a column of the list. <br /> <br />|A numeric value that is the accumulated sum. <br /> <br />When using a List, an arithmetic expression using the different columns in the List can also return a numeric value.  The Lists are written as **item.&#42;ColumnName&#42;**. <br /> <br />|
|Cumulative Average <br /> <br />|Returns the accumulated average value of a record. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input:* <br /> <br />A link from a tree node or a List operation that contains a numeric value. When using a List operation, the Cumulative operation can operate on a column of the list. <br /> <br />|A numeric value that is the accumulated average. <br /> <br />|
|Cumulative Concatenate <br /> <br />|Concatenate strings from a record in the source schema to a single record in the target schema. <br /> <br />|Can have one and two input parameters: <br /> <br />*Input:* <br /> <br />A link from a tree node or a List operation that contains a string value. When using a List operation, the Cumulative operation can operate on a column of the list. <br /> <br />*Separator:* <br /> <br />Delimits the string values. <br /> <br />|A string value that has been accumulated and concatenated. <br /> <br />|
|Cumulative Maximum <br /> <br />|Returns the accumulated maximum value of a record. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input:* <br /> <br />A link from a tree node or a List operation that contains a numeric value. When using a List operation, the Cumulative operation can operate on a column of the list. <br /> <br />|A numeric value that is the maximum value. <br /> <br />|
|Cumulative Minimum <br /> <br />|Returns the accumulated minimum value of a record. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input:* <br /> <br />A link from a tree node or a List operation that contains a numeric value. When using a List operation, the Cumulative operation can operate on a column of the list. <br /> <br />|A numeric value that is the minimum value. <br /> <br />|
|Cumulative Count <br /> <br />|Returns the number of times a specified repeating structure or value occurs. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input:* <br /> <br />A link from a tree node or a List operation. When using a List operation, the Cumulative operation can operate on a column of the list. <br /> <br />|A numeric value is the total count a repeating value occurs. <br /> <br />|

## Error and Data Handling
[!INCLUDE[af_integration](/Token/af_integration_md.md)] provides the ability to configure how an error is handled and how an empty or null node is handled. The error handling behavior of the following **Cumulative**[!INCLUDE[mapop](/Token/mapop_md.md)]s is configurable:

- **Cumulative Sum**

- **Cumulative Minimum, Maximum and Average**

Steps:

1. Open a **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]** or the **BizTalk Service Artifacts** project in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)].

2. Double-click a [!INCLUDE[transform](/Token/transform_md.md)] (.trfm) to open the [!INCLUDE[transform](/Token/transform_md.md)] Designer.

3. In the [!INCLUDE[transform](/Token/transform_md.md)] toolbar, select **Settings**.

**Error Handling tab**

In the **Error Handling** tab, the following **Cumulative**[!INCLUDE[mapop](/Token/mapop_md.md)]s have three **Behavior** options:

- **Cumulative Sum**:

   - **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and the error is then sent back to the client that sent the message.

   - **Output default value NaN**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, NaN (Not a Number) is returned as the output.

   - **Output default value 0**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, zero (0) is returned as the output.

- **Cumulative Minimum, Maximum and Average**:

   - **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and the error is then sent back to the client that sent the message.

   - **Output default value NaN**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, NaN (Not a Number) is returned as the output.

   - **Output default value 0**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, zero (0) is returned as the output.

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

[Date &#47; Time Map Operations - Usage and Examples](/Topic/Date_/_Time_Map_Operations_-_Usage_and_Examples.md)

[Miscellaneous Map Operations - Usage and Examples](/Topic/Miscellaneous_Map_Operations_-_Usage_and_Examples.md)

## See Also
[Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md)

