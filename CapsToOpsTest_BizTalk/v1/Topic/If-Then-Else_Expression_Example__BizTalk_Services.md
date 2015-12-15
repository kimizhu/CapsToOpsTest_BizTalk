---
description: na
keywords: na
pagetitle: If-Then-Else Expression Example: BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48b5f6a2-990d-4026-b798-2d83d3dfb69f
---
# If-Then-Else Expression Example: BizTalk Services
Lists If-Then-Else example in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)].

## If-Then-Else Expression Example
There is a **Zip** field in the input document and a **State** field in the output document. If the **Zip** is 98052 in the input document, then the **State** field in the output document is updated with **WA**. If the **Zip** is not 98052, **State** is updated with **Other**.

To do this, add an If-Then-Else Expression [!INCLUDE[mapop](/Token/mapop_md.md)] to the [!INCLUDE[transform](/Token/transform_md.md)]:

1. Drag the If-Then-Else Expression to the [!INCLUDE[transform](/Token/transform_md.md)] Designer area.

2. Create a link from the **Zip** field in the input document to this If-Then-Else Expression.

3. Create a link from the **State** field in the output document to this If-Then-Else Expression.

4. Configure the If-Then-Else Expression with the following parameters:

   |||
   |-|-|
   |*Zip* <br /> <br />The *input* name will be displayed as the node name it is connected to in the input document. <br /> <br />|Zip <br /> <br />|
   |*Condition* <br /> <br />|Zip == 98052 <br /> <br />|
   |*Then Value* <br /> <br />|“WA” <br /> <br />|
   |*Else Value* <br /> <br />|“Other” <br /> <br />|

With this [!INCLUDE[transform](/Token/transform_md.md)], the **State** node in the output is populated with **WA** if the zip code is 98052. If the zip code is not 98052, the **State** node is populated with **Other**.

## Error and Data Handling
If an error occurs with an **If-Then-Else Expression**[!INCLUDE[mapop](/Token/mapop_md.md)], by default, the entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. This error handling behavior is configurable. See **Error and Data Handling** at [Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md).

## See Also
[Arithmetic Expression Examples: BizTalk Services](/Topic/Arithmetic_Expression_Examples__BizTalk_Services.md)
[Logical Expression Examples: BizTalk Services](/Topic/Logical_Expression_Examples__BizTalk_Services.md)
[Conditional Assignment Example: BizTalk Services](/Topic/Conditional_Assignment_Example__BizTalk_Services.md)
[Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md)

