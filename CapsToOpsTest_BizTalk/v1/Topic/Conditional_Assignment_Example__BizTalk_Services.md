---
description: na
keywords: na
pagetitle: Conditional Assignment Example: BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b048e49-16ca-4b65-90ee-43e4fd99d454
---
# Conditional Assignment Example: BizTalk Services
Lists a Conditional Assignment example in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)].

## Conditional Assignment Example
The input document has a **Person** node with a **Title** field. The output document also has a **Title** field. The goal is for the **Title** field in the output document be created *only* if **Title** exists in the input document **and** if the **Title** field is not null.

To do this, use the Conditional Assignment [!INCLUDE[mapop](/Token/mapop_md.md)]:

1. Drag the Conditional Assignment [!INCLUDE[mapop](/Token/mapop_md.md)] to the [!INCLUDE[transform](/Token/transform_md.md)] Designer area.

2. Create a link from the **Title** field in the output document to this Conditional Assignment [!INCLUDE[mapop](/Token/mapop_md.md)].

3. Add a Logical Expression [!INCLUDE[mapop](/Token/mapop_md.md)] and do the following:

   - Create a link from the **Title** field in the input document to this Logical Expression [!INCLUDE[mapop](/Token/mapop_md.md)].

   - Configure the Logical Expression [!INCLUDE[mapop](/Token/mapop_md.md)] to state: **Exists(Title) &amp;&amp; !IsEmpty(Title)**

   - Create a link from the output of this Logical Expression as the first input to the Conditional Assignment [!INCLUDE[mapop](/Token/mapop_md.md)].

4. Create a link from the **Title** field in the input document to the Conditional Assignment [!INCLUDE[mapop](/Token/mapop_md.md)].

With this [!INCLUDE[transform](/Token/transform_md.md)], the **Title** node in the output is created **only** if the **Title** node in the input document exists and is non-empty.

## See Also
[Arithmetic Expression Examples: BizTalk Services](/Topic/Arithmetic_Expression_Examples__BizTalk_Services.md)
[Logical Expression Examples: BizTalk Services](/Topic/Logical_Expression_Examples__BizTalk_Services.md)
[If-Then-Else Expression Example: BizTalk Services](/Topic/If-Then-Else_Expression_Example__BizTalk_Services.md)
[Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md)

