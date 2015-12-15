---
description: na
keywords: na
pagetitle: Transforms/Maps Best Practices
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 925b32e1-5ac6-48b4-8028-d66ffc245fad
---
# Transforms/Maps Best Practices


|||
|-|-|
|**Label and Comment Properties** <br /> <br />|When configuring a [!INCLUDE[mapop](/Token/mapop_md.md)], modify the **Label** property to name each [!INCLUDE[mapop](/Token/mapop_md.md)]. Populate the **Comment** property with specific details, especially the MapEach and ForEach [!INCLUDE[mapop](/Token/mapop_md.md)]s: <br /> <br />See Image 1, below <br /> <br />This **Label** name is used in the breadcrumb trail. It is very important to change the **Label** name. <br /> <br />Also, the **Search** feature can be used to find a specific [!INCLUDE[mapop](/Token/mapop_md.md)] by the **Label** name or text within the **Comment** property. <br /> <br />|
|**Breadcrumb Trail** <br /> <br />|When creating links and adding [!INCLUDE[mapop](/Token/mapop_md.md)]s, use the Breadcrumb trail to determine the current scope container. At the bottom of the [!INCLUDE[transform](/Token/transform_md.md)] Design surface, the scope hierarchy is displayed in the breadcrumb trail. The current scope is the last item in the breadcrumb trail. When a MapEach Loop scope is set, the breadcrumb trail is updated to reflect the current hierarchy. <br /> <br />In the example below, the Employee Mapping MapEach Loop is the last item in the breadcrumb trail so it is the current set scope. Any [!INCLUDE[mapop](/Token/mapop_md.md)]s added or links created are under the Employee Mapping scope: <br /> <br />See Image 2, below <br /> <br />[Using Scope in a Loop - How To](/Topic/Using_Scope_in_a_Loop_-_How_To.md) provides more specific details. <br /> <br />|
|**Sample Input File** <br /> <br />|Before starting to create a [!INCLUDE[transform](/Token/transform_md.md)], have a sample input.xml file ready to test the [!INCLUDE[transform](/Token/transform_md.md)]. <br /> <br />|
|**Build in Increments** <br /> <br />|Build the [!INCLUDE[transform](/Token/transform_md.md)] incrementally. Once portions of the [!INCLUDE[transform](/Token/transform_md.md)] are built, save it and fix any errors. Test the [!INCLUDE[transform](/Token/transform_md.md)] using the **Test Map** feature. <br /> <br />|
|**Set Scope** <br /> <br />|Set the correct working scope container when creating a [!INCLUDE[transform](/Token/transform_md.md)]. Remember, working scope is indicated by the last item in the breadcrumb trail at the top of the [!INCLUDE[transform](/Token/transform_md.md)] Designer surface. To set scope, refer to [Using Scope in a Loop - How To](/Topic/Using_Scope_in_a_Loop_-_How_To.md). <br /> <br />|
|**Creating Links** <br /> <br />|Creating a link from a source to a target is left to right. Any link made from right to left considers left as the source and right as the target. Any link made from left to right considers left as the source and right as the target. <br /> <br />|
|**Direct Links** <br /> <br />|To link source and target nodes with similar node structure or node names, use the **Direct Link** feature. **Direct Linking** can be used with repeating records and non-repeating records. See [Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md) for more information. <br /> <br />|
|**Test the Transform** <br /> <br />|Use the **Test Map Input File** and **Test Map Output File** properties of the [!INCLUDE[transform](/Token/transform_md.md)] in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)]: <br /> <br /><ol><li>Select the [!INCLUDE[transform](/Token/transform_md.md)] (.trfm) file in Solution Explorer. </li><li>In **Properties**, click **Test Map Input File** and browse to the sample input.xml. Click **Open**. </li><li>In **Properties**, click **Test Map Output File** and browse to the sample output.xml. Click **Open**. </li><li>Right-click the [!INCLUDE[transform](/Token/transform_md.md)] in Solution Explorer and select **Test Map**. </li> </ol>The Output window displays the result. **Tip:** If a [!INCLUDE[transform](/Token/transform_md.md)] contains a **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)], a **Test Data for context property** window displays. In this window, you can enter a temporary value for the context property to test the [!INCLUDE[transform](/Token/transform_md.md)]. <br />|
Image 1

![](/Image/AppFabricIntTrans_LabComments.gif)

Image 2

![](/Image/AppFabricIntBreadcrumbTrail.gif)

**SCOPE/LOOP BEST PRACTICES**

|||
|-|-|
|**Containing Scope** <br /> <br />|Every [!INCLUDE[mapop](/Token/mapop_md.md)] and link has a **Containing Scope** property. The **Containing Scope** property indicates the parent scope container. Use this property to help determine the current parent scope container. <br /> <br />|
|**Container** <br /> <br />|Each container can be minimized and expanded. Setting scope on a MapEach Loop can be done when the container is expanded. Modifying links are done when the container is minimized or expanded. Minimizing the container automatically unsets the scope. <br /> <br />Minimizing the container also provides a larger design surface. <br /> <br />|
|**Ambiguous Links** <br /> <br />|If the [!INCLUDE[transform](/Token/transform_md.md)] Designer determines that the scope of a link or a [!INCLUDE[mapop](/Token/mapop_md.md)] is ambiguous when the link or [!INCLUDE[mapop](/Token/mapop_md.md)] is created, an error is flagged when compiled. All errors are flagged during [!INCLUDE[transform](/Token/transform_md.md)] compilation and when loading a fresh [!INCLUDE[transform](/Token/transform_md.md)]. <br /> <br />|
|**Error &amp; Data Handling** <br /> <br />|Error Handling and Null/Empty Data Handling behavior is configurable for the [!INCLUDE[transform](/Token/transform_md.md)] Runtime. To customize how your application handles these scenarios, configure these settings in the individual [!INCLUDE[mapop](/Token/mapop_md.md)]s in the [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] project. <br /> <br />|
|**Home Link** <br /> <br />|Selecting **Home** in the breadcrumb trail puts the [!INCLUDE[transform](/Token/transform_md.md)] at the Home (Page) scope. No scope is set and the **Containing Scope** property displays None. <br /> <br />|
|**Move To Working Scope** <br /> <br />|When moving links and [!INCLUDE[mapop](/Token/mapop_md.md)]s, refer to the highlight propagation and the **Containing Scope** property to determine the parent and child scope containers. <br /> <br />|
|**Sibling and Children** <br /> <br />|Operations in a scope can use the source elements and [!INCLUDE[mapop](/Token/mapop_md.md)]s available in its scope and its parent hierarchy. Elements and [!INCLUDE[mapop](/Token/mapop_md.md)]s in a sibling or child scope cannot be used. <br /> <br />|
|**Ctrl + Select** <br /> <br />|To move [!INCLUDE[mapop](/Token/mapop_md.md)]s and their links, use **Ctrl + Click** to select the items to move. **Ctrl + Click** cuts the items and then you paste to the desired location. <br /> <br />|
|**Repeating Record with Direct Linking** <br /> <br />|Draw a link from a repeating record in the source document to the repeating record in the target document. When doing this, you can create direct links by node name and structure. For other options, go to [Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md). <br /> <br />|

## More Transforms topics
[Convert a BizTalk map to a BizTalk Services Transform](/Topic/Convert_a_BizTalk_map_to_a_BizTalk_Services_Transform.md)

[Use standard XSD constructs in your maps](/Topic/Use_standard_XSD_constructs_in_your_maps.md)

[Loop and Scope Examples in map or transforms](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md)

**[Azure BizTalk Services Resources on the TechNet Wiki](http://social.technet.microsoft.com/wiki/contents/articles/11426.azure-biztalk-services-resources-on-the-technet-wiki.aspx)**

