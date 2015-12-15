---
description: na
keywords: na
pagetitle: Loop Map Operations - Usage and Examples
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42b6bb45-6c49-466a-aed6-88811f0e40a1
---
# Loop Map Operations - Usage and Examples

## Loop [!INCLUDE[mapop](/Token/mapop_md.md)]s
There are two Loop [!INCLUDE[mapop](/Token/mapop_md.md)]s in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]: **ForEach Loop** and **MapEach Loop**. Loop [!INCLUDE[mapop](/Token/mapop_md.md)]s provide the following benefits:

- When an input message contains repeating elements, a Loop flattens the hierarchy in the output document.

- To perform data manipulation, like concatenating fields or applying a mathematical formula, a Loop can use an expression and output the results.

- A Loop filters an input document based on criteria and outputs the filtered data.

Loop [!INCLUDE[mapop](/Token/mapop_md.md)]s:

|Map Operator <br /> <br />|Description <br /> <br />|Parameters <br /> <br />|Output <br /> <br />|
|----------------|---------------|--------------|----------|
|ForEach Loop <br /> <br />|Loops over a repeating record in the source document. Relationships defined within the ForEach Loop container are evaluated at each iteration of the loop. There is no record in the target document and there are no output links. <br /> <br />ForEach is typically used to flatten a source loop hierarchy. It cannot output a record. <br /> <br />|Requires one input parameter and one optional parameter: <br /> <br />*Source:* <br /> <br />Required. A repeating record in the source document or a List [!INCLUDE[mapop](/Token/mapop_md.md)]. <br /> <br />*Condition:* <br /> <br />Optional. Acts as a filter for the records to iterate. <br /> <br />|None <br /> <br />|
|MapEach Loop <br /> <br />|Loops over a repeating record in the source document. Relationships defined within the MapEach Loop container scope are evaluated at each iteration of the loop. Each iteration of the loop produces an instance of the repeating record in the target document. <br /> <br />|Requires one input parameter and one optional parameter: <br /> <br />*Source:* <br /> <br />Required. A repeating record in the source document or a List [!INCLUDE[mapop](/Token/mapop_md.md)]. <br /> <br />*Condition:* <br /> <br />Optional. Acts as a filter for the records to iterate. <br /> <br />|A record is created in the target document. <br /> <br />|

## Set Scope with Direct Links
The ForEach Loop and MapEach Loop have a container. All [!INCLUDE[mapop](/Token/mapop_md.md)]s added to the container execute in the scope of that Loop container.

In addition to the Loop container, the MapEach Loop has the Set Scope icon: ![](/Image/PinnedScope.bmp). When a MapEach Loop is added to the [!INCLUDE[transform](/Token/transform_md.md)] design area, Set Scope is automatic, as indicated by the arrow ![](/Image/PinnedScope.bmp). To work in the Home container or any other container, select the arrow to unset the Set Scope icon: ![](/Image/UnpinnedScope.bmp).

When linking a repeating record in the source document to a repeating record in the target document, a MapEach Loop is needed. Creating these links from each source node to the target node is often time consuming. As a result, [!INCLUDE[af_integration](/Token/af_integration_md.md)] includes Direct Link functionality. Direct Linking includes the following features:

- Automatically does a bulk direct link of a repeating record and its nodes on the source schema to the target schema.

- A MapEach Loop (with Set Scope enabled) is automatically created when you link repeating records in the source schema to repeating records in the target schema.

- Automatically does a bulk direct link of non-repeating records and its nodes on the source schema to the target schema.

#### To use the Direct Link functionality of a repeating record

1. Draw a link from a repeating record in the source document to the repeating record in the target document.

2. A dialog window displays the following options:

   |Option <br /> <br />|Description <br /> <br />|
   |----------|---------------|
   |Simple Link <br /> <br />|Creates a link between the repeating records. The node links under the repeating record are not created. A MapEach Loop is not created. <br /> <br />|
   |Map Each <br /> <br />|Adds a MapEach Loop (with Set Scope enabled) and creates a link between the two repeating records. Node links under the repeating records are not created. <br /> <br />|
   |Link by Structure <br /> <br />|Adds a MapEach Loop (with Set Scope enabled) and creates a bulk link between the repeating records and their node links. <br /> <br />A MapEach Loop is created for every link between the source and target repeating records. <br /> <br />|
   |Link by Name <br /> <br />|Adds a MapEach Loop (with Set Scope enabled) and creates a bulk link between the repeating records and their node links that have the same name. <br /> <br />A MapEach Loop is created for every link between the source and target repeating records. <br /> <br />If the names do not match, a link is created between the two repeating records in the MapEach Loop. Node links under the repeating records are not created. <br /> <br />|
   |Cancel <br /> <br />|Cancels the link and returns to the Home container. <br /> <br />|
   > [!WARNING]
   > A MapEach Loop is only used when creating a link between repeating records in the source and target schemas. If the source **or** target record is non-repeating, a MapEach Loop is not automatically created. In this situation, create the links under the scope of an existing MapEach Loop.

#### To use the Direct Link functionality of a non-repeating record

1. Draw a link from a repeating record in the source document to a non-repeating record in the target document.

   **OR**, draw a link from a non-repeating record in the source document to a repeating record in the target document.

2. A dialog window displays the following options:

   |Option <br /> <br />|Description <br /> <br />|
   |----------|---------------|
   |Simple Link <br /> <br />|Creates a link between the records. The node links under the records are not created. <br /> <br />|
   |Link by Structure <br /> <br />|Creates a bulk link between the records and their node links. <br /> <br />|
   |Link by Name <br /> <br />|Creates a bulk link between the records and their node links that have the same name. <br /> <br />If the names do not match, a link is not created between the two records. Node links under a record are not created. <br /> <br />|
   |Cancel <br /> <br />|Cancels the link and returns to the Home container. <br /> <br />|
   > [!WARNING]
   > A MapEach Loop is only used when creating a link between repeating records in the source and target schemas. If the source **or** target record is non-repeating, a MapEach Loop is not automatically created. In this situation, create the links under the scope of an existing MapEach Loop.

## In This Section
[Using Scope in a Loop - How To](/Topic/Using_Scope_in_a_Loop_-_How_To.md)

## Additional [!INCLUDE[mapop](/Token/mapop_md.md)]s
[String Map Operations - Usage and Examples](/Topic/String_Map_Operations_-_Usage_and_Examples.md)

[Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md)

[List Map Operations - Usage and Examples](/Topic/List_Map_Operations_-_Usage_and_Examples.md)

[Cumulative Map Operations - Usage and Examples](/Topic/Cumulative_Map_Operations_-_Usage_and_Examples.md)

[Date &#47; Time Map Operations - Usage and Examples](/Topic/Date_/_Time_Map_Operations_-_Usage_and_Examples.md)

[Miscellaneous Map Operations - Usage and Examples](/Topic/Miscellaneous_Map_Operations_-_Usage_and_Examples.md)

## See Also
[Loop and Scope Examples in map or transforms](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md)

