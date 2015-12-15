---
description: na
keywords: na
pagetitle: Loop and Scope Examples in map or transforms
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7187a87-6560-43b3-a38f-5e3274012171
---
# Loop and Scope Examples in map or transforms
Lists examples of Scope and Loop operations in [!INCLUDE[af_integration](/Token/af_integration_md.md)]. Specifically:

[Scope Example](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md#BKMK_ScopeEx)

[ForEach Loop Example](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md#BKMK_ForEachEx)

[MapEach Loop Example](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md#BKMK_MapEachEx)

## <a name="BKMK_ScopeEx"></a>Scope Example
In the following example, a **Company Mapping** MapEach Loop [!INCLUDE[mapop](/Token/mapop_md.md)] contains the **Dept Loop** ForEach Loop [!INCLUDE[mapop](/Token/mapop_md.md)] within its scope container. This **Dept Loop** ForEach Loop contains the **Employee Mapping** MapEach Loop within its scope container.

In this example, every time a **Company** and a **Department** name are in the input data file, this [!INCLUDE[transform](/Token/transform_md.md)] generates the **Company** and **Employee** output records:

![](/Image/AppFabricIntScopeExample.jpg)

## <a name="BKMK_ForEachEx"></a>ForEach Loop Example
There is a **Department** source schema with **Name**, **Size** and **Employee** records. **Employee** has the **Name** and **Details** fields. The hierarchy formed is:

```
Department
   Name
   Size
   Employee
      Name
      Details
```
Employee{Name, Details} is mapped to Employee{Name, Details} in the target schema.

The goal is to flatten all Departments where the Size &lt; 10. To achieve this, do the following:

#### To configure the [!INCLUDE[transform](/Token/transform_md.md)]

1. Add a ForEach Loop to the [!INCLUDE[transform](/Token/transform_md.md)] design surface.

2. Create a link from Department in the source schema to this ForEach Loop.

3. Add a Logical Expression [!INCLUDE[mapop](/Token/mapop_md.md)] to the Home (Page) container. Configure the expression to state: **Size&lt;10**.

4. Create a link from this Logical Expression to the ForEach Loop.

5. Under the ForEach scope container, add a MapEach Loop to the [!INCLUDE[transform](/Token/transform_md.md)] design surface.

6. Create a link from Employee in the source schema to this MapEach Loop.

7. Create a link from the MapEach Loop to Employee on the target schema.

8. Create the appropriate links for the Employee Name and Employee Details fields.

With this [!INCLUDE[transform](/Token/transform_md.md)], the ForEach Loop  iterates over the Department source record. For those Departments that have &lt; 10 Employees, the MapEach Loop iterates on the Employee repeating record and populates the Employee Name and Employee Details fields in the target document.

[Logical Expression Examples: BizTalk Services](/Topic/Logical_Expression_Examples__BizTalk_Services.md) provides more information on the Logical Expression [!INCLUDE[mapop](/Token/mapop_md.md)].

## <a name="BKMK_MapEachEx"></a>MapEach Loop Example
There is a source schema with an **Employee** record. **Employee** has a **Details** record and **Details** has an **Age** field. The hierarchy formed is:

```
Employee
   Details
      Age
```
The target schema has the same structure.

The goal is to not emit records where Age &gt; 100. To achieve this, do the following:

#### To configure the [!INCLUDE[transform](/Token/transform_md.md)]

1. Add a MapEach Loop to the [!INCLUDE[transform](/Token/transform_md.md)] design surface.

2. Create a link from Employee in the source schema to this MapEach Loop.

3. Add a Logical Expression [!INCLUDE[mapop](/Token/mapop_md.md)] to the Home (Page) container. Configure the expression to state: **Age &lt; 100**.

4. Create a link from this Logical Expression to the MapEach Loop.

5. Create a link from Employee in the target schema to the MapEach Loop.

With this [!INCLUDE[transform](/Token/transform_md.md)], the MapEach Loop [!INCLUDE[mapop](/Token/mapop_md.md)] creates the Employee record in the target document for those employees where Age &lt; 100.

[Logical Expression Examples: BizTalk Services](/Topic/Logical_Expression_Examples__BizTalk_Services.md) provides more information on the Logical Expression [!INCLUDE[mapop](/Token/mapop_md.md)].

## More Examples

- For the Expression [!INCLUDE[mapop](/Token/mapop_md.md)]s examples, see [Arithmetic Expression Examples: BizTalk Services](/Topic/Arithmetic_Expression_Examples__BizTalk_Services.md), [Logical Expression Examples: BizTalk Services](/Topic/Logical_Expression_Examples__BizTalk_Services.md), [If-Then-Else Expression Example: BizTalk Services](/Topic/If-Then-Else_Expression_Example__BizTalk_Services.md), and [Conditional Assignment Example: BizTalk Services](/Topic/Conditional_Assignment_Example__BizTalk_Services.md).

## More Transforms topics
[Convert a BizTalk map to a BizTalk Services Transform](/Topic/Convert_a_BizTalk_map_to_a_BizTalk_Services_Transform.md)

[Use standard XSD constructs in your maps](/Topic/Use_standard_XSD_constructs_in_your_maps.md)

[Transforms&#47;Maps Best Practices](/Topic/Transforms/Maps_Best_Practices.md)

**[Azure BizTalk Services Resources on the TechNet Wiki](http://social.technet.microsoft.com/wiki/contents/articles/11426.azure-biztalk-services-resources-on-the-technet-wiki.aspx)**

## See Also
[Using Scope in a Loop - How To](/Topic/Using_Scope_in_a_Loop_-_How_To.md)
[Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md)

