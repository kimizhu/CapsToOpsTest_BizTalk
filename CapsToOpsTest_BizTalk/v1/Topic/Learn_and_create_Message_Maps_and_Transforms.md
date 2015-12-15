---
description: na
keywords: na
pagetitle: Learn and create Message Maps and Transforms
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8543a8b-269d-4d11-abfa-68ddf2435bec
---
# Learn and create Message Maps and Transforms
[!INCLUDE[transform](/Token/transform_md.md)]s in **[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]** are designed to manipulate data. Consider the following scenario:

An incoming message contains customer data, including First Name, Last Name, Street Address, City, State, and Zip Code. When this data is received, you want to manipulate the data. For example, you want to combine First Name and Last Name into a single Name value.

[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] is your answer. Using a [!INCLUDE[transform](/Token/transform_md.md)], the incoming message data can be manipulated to the desired output.

## Benefits

- **XSLT Support**: You can:

   - Import an .xslt or .xsl file or directly enter XSLT syntax

   - Import an XML extension file or directly enter XML syntax

   - Use the XslCompiledTransform property for better performance

   - Use XSLT in every Transform file (.trfm)

   > [!TIP]
   > When XSLT is used, the [!INCLUDE[transform](/Token/transform_md.md)] design area is grayed out.

- **Built-in [!INCLUDE[mapop](/Token/mapop_md.md)]s**: Many [!INCLUDE[transform](/Token/transform_md.md)] scenarios are handled by the built-in [!INCLUDE[mapop](/Token/mapop_md.md)]s, including string manipulation, looping with set scope, expressions, list functionality, Date/Time, CSharp scripting, and so on.

- **xs:extension and xs:restriction**: Use complex types in your schemas.

- **Choose your project**: In [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], you can create a new [!INCLUDE[transform](/Token/transform_md.md)] in its own project (**BizTalk Service Artifacts**) or create a new [!INCLUDE[transform](/Token/transform_md.md)] in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. When created in its own project, a [!INCLUDE[transform](/Token/transform_md.md)] can be added to an X12 agreement between EDI partners.

- **Add the [!INCLUDE[transform](/Token/transform_md.md)] to a [!INCLUDE[bridge](/Token/bridge_md.md)]**: After a [!INCLUDE[transform](/Token/transform_md.md)] is created, the [!INCLUDE[transform](/Token/transform_md.md)] can be added to the [!INCLUDE[transform](/Token/transform_md.md)] stage within a [!INCLUDE[one-way](/Token/one-way_md.md)] or a [!INCLUDE[request_response](/Token/request_response_md.md)].

   [Create an XML One-Way Bridge](/Topic/Create_an_XML_One-Way_Bridge.md) and [Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md) lists the steps.

## Get Started
[Convert a BizTalk map to a BizTalk Services Transform](/Topic/Convert_a_BizTalk_map_to_a_BizTalk_Services_Transform.md)

[Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md)

[Use standard XSD constructs in your maps](/Topic/Use_standard_XSD_constructs_in_your_maps.md)

[Transforms&#47;Maps Best Practices](/Topic/Transforms/Maps_Best_Practices.md)

[Loop and Scope Examples in map or transforms](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md)

## See Also
[What are Bridges?](/Topic/What_are_Bridges_.md)
[Uses and Stages of Bridges](/Topic/Uses_and_Stages_of_Bridges.md)

