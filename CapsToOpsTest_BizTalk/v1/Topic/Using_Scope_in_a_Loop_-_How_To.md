---
description: na
keywords: na
pagetitle: Using Scope in a Loop - How To
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a57af82-cae8-412d-a066-fb6a766d0be1
---
# Using Scope in a Loop - How To
This topic describes using scope in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)].

## Scope [!INCLUDE[transform](/Token/transform_md.md)] Design Area
![](/Image/AppFabricIntScopeDesignSurface.jpg)

### Breadcrumb Trail
At the bottom of the [!INCLUDE[transform](/Token/transform_md.md)] Design area, the MapEach Loop scope hierarchy is displayed in the breadcrumb trail. The current MapEach Loop scope is the last item in the breadcrumb trail. When scope is set in a MapEach Loop, the breadcrumb trail is updated to reflect the current hierarchy. In the following example, **Employee Mapping** is the last MapEach Loop in the breadcrumb trail so it is the current set scope:

![](/Image/AppFabricIntBreadcrumbTrail.gif)

### Container
The MapEach Loop, ForEach Loop, and Create List operations have a container. The child objects are grouped together in the container. Items within the container are in the scope of the container and are executed within the scope of the container. An inner container is a child of the outer container. When a container is selected, a solid line is displayed around the container. In the following example, **Dept Mapping** is selected so its container has the solid line:

![](/Image/Container.bmp)

#### Collapse and Expand
Each container can be collapsed and expanded in two ways:

- Select the container and press the SPACE bar.

- Select the minus (-) to collapse and the plus sign (+) to expand.

Collapsing the container automatically unsets the MapEach Loop scope. Adding [!INCLUDE[mapop](/Token/mapop_md.md)]s to a container can only be done when the container is expanded. Modifying links can be done when the container is collapsed or expanded. In the following example, **Employee Mapping** is collapsed and the **Containing Scope** property automatically goes to its parent node, which is **Dept Mapping**:

![](/Image/Minimized.jpg)

**Container Header**

When the MapEach scope is set, the container header is highlighted. These colors are modified using the following steps:

1. Go to the **Tools** menu and select **Options**.

2. Expand **[!INCLUDE[transform](/Token/transform_md.md)]s Designer** and select **Colors &amp; Fonts**.

3. Select **Working Scope Header Background** to change its color.

4. Select **OK**.

### Direct Links with Repeating Records
When linking a repeating record in the source document to a repeating record in the target document, a MapEach Loop is needed. Creating these links from each source node to the target node is often time consuming. As a result, [!INCLUDE[af_integration](/Token/af_integration_md.md)] includes Direct Link functionality.

Direct Linking is simply copying from an input node to an output node, with no other processing. Direct Linking is also used when linking non-repeating records; which does not require a MapEach Loop.

[Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md) describes the Direct Link functionality.

### Page
Container Scope is per Page. When scope is set on a MapEach Loop in Page 1, selecting Page 2 sets scope on Home in Page 2.

### Highlight Propagation
When you select a container, the source and target node links are highlighted in green. In the following example, the **Company Mapping**, **Dept Mapping**, and **Employee Mapping** scopes are set. The breadcrumb trail shows the MapEach Loop hierarchy. **Employee Mapping** is the last item in the breadcrumb trail and is therefore the current scope. The **Employee Mapping** node is highlighted in green:

![](/Image/AppFabricIntScopeIndicLinks.jpg)

##### To modify or turn off the highlighting

1. On the **Tools** menu, select **Options**.

2. Select **Transforms Designer**.

3. To turn off the highlighting feature, select **General**, and clear the **Highlight Propagation** option.

4. To modify the highlighting colors, select **Colors &amp; Fonts**.

### Containing Scope
When a child loop is selected, the **Containing Scope** property is updated with the Label name of the parent scope. In the following example, **Dept Mapping** is selected, and the **Containing Scope** property displays **Company Mapping**, which is the parent node:

![](/Image/AppFabricIntLoopIndicProperty.jpg)

### Home
Selecting **Home** in the breadcrumb trail puts the scope at the Page. No scope is set and the **Containing Scope** property displays None:

![](/Image/AppFabricIntHome_Breadcrumb.jpg)

### Cut, Copy &amp; Paste
[!INCLUDE[mapop](/Token/mapop_md.md)]s are movable using Cut/Copy and Paste. Links are not movable using Cut/Copy and Paste. If you move a [!INCLUDE[mapop](/Token/mapop_md.md)] using Cut/Copy and Paste, the links are removed.

To move [!INCLUDE[mapop](/Token/mapop_md.md)]s and their links, use **Ctrl + Click** to select the items to move. **Ctrl + Click** cuts the items and then you paste to the desired location. [!INCLUDE[mapop](/Token/mapop_md.md)]s and links cannot be dragged and dropped.

### Exit a Scope
To exit a MapEach Loop scope, do any of the following:

- Unset scope ![](/Image/UnpinnedScope.bmp). This option moves the focus up one MapEach Loop scope in the hierarchy.

   In the following example,  scope is set:

   ![](/Image/AppFabricIntLoopIndicProperty.jpg)

   Then, the **Employee Mapping** MapEach Loop scope is unset. The **Dept Mapping** MapEach Loop scope is the last item in the breadcrumb trail and is the current scope:

   ![](/Image/AppFabricIntExit_Unpinned.jpg)

- Select any parent scope in the breadcrumb trail. For example, select Dept Mapping in the Breadcrumb Trail:

   ![](/Image/AppFabricInt.jpg)

- Set a different scope.

## In This Section
For the best practices when working with Container Scope and a Scope Example, refer to the following topics:

[Transforms&#47;Maps Best Practices](/Topic/Transforms/Maps_Best_Practices.md)

[Loop and Scope Examples in map or transforms](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md)

## See Also
[Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md)

