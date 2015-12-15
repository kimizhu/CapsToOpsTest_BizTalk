---
description: na
keywords: na
pagetitle: Step 5: Transform the Flat File Schema to the Insert Schema for OrderDetails Table
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7287db8a-eb40-4e5a-a97b-83b9be793718
---
# Step 5: Transform the Flat File Schema to the Insert Schema for OrderDetails Table
This topic lists the steps to create a [!INCLUDE[transform](/Token/transform_md.md)] to map the flat-file message schema to the schema of an **Insert** operation on the **OrderDetails** table in [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)]. Before we create a [!INCLUDE[transform](/Token/transform_md.md)], let’s have a look at the two schemas and then let’s understand what needs to be done as part of the [!INCLUDE[transform](/Token/transform_md.md)].

Here’s a snapshot of the two schemas:

![](/Image/AFINT_FTPTut_Schemas.gif)

The following table lists the mapping requirements and the [!INCLUDE[mapop](/Token/mapop_md.md)]s using which this is accomplished:

|What to map? <br /> <br />|How to achieve? <br /> <br />|
|----------------|-------------------|
|**OrderId** node in the source schema maps directly to **OrderId** node in the destination schema. <br /> <br />|You directly connect the two nodes in the two schemas. <br /> <br />|
|Because **OrderDetails** node in the flat-file schema is a repeating node, all the values in the **Quantity** node should be added up and the cumulative value should be passed on to the **QuantityOrdered** node in the destination schema. <br /> <br />|You connect the **Quantity** and **QuantityOrdered** nodes using a **Cumulative Sum**[!INCLUDE[mapop](/Token/mapop_md.md)]. <br /> <br />|
|The **TotalAmount** node in the destination schema must contain the cumulative value of all (**Unit Price** &#42; **Quantity**). <br /> <br />|Instructions on how to set this are provided at [To map to the TotalAmount element](/Topic/Step_5__Transform_the_Flat_File_Schema_to_the_Insert_Schema_for_OrderDetails_Table.md#BKMK_TotalAmount) <br /> <br />|

### To map to the TotalAmount element

1. In [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], right click the **FTP_EAI_Tutorial** project, point to **Add**, and then select **New Item**.

2. In **Add New Item**, select **Map**, enter **Map.trfm** as the map name, and then select **OK**.

3. In Solution Explorer, double click the **Map.trfm** file to open the [!INCLUDE[transform](/Token/transform_md.md)]. On the [!INCLUDE[transform](/Token/transform_md.md)] design area, set the source schema to **PO.xsd** and set the destination schema to **FTPEAITutorial_TableOperation.dbo.OrderDetails.xsd**.

4. On the **Toolbox**, from the **List Operations** category, drag-and-drop a **Create List**[!INCLUDE[mapop](/Token/mapop_md.md)] on the [!INCLUDE[transform](/Token/transform_md.md)] design area. Double-click the [!INCLUDE[mapop](/Token/mapop_md.md)], select the plus sign, and enter **Amount** as the member name. Enter the **Member Type** as **Number** and then select **OK**.

   By doing this, you are creating an in-memory variable called **Amount**.

5. Within a **List**[!INCLUDE[mapop](/Token/mapop_md.md)], add a **ForEach Loop**[!INCLUDE[mapop](/Token/mapop_md.md)], and then connect it to the **OrderDetails** element in the source schema. You do so because **OrderDetails** element is a repeating element in the message schema.

6. Within a **ForEach Loop**[!INCLUDE[mapop](/Token/mapop_md.md)], add an **Arithmetic Expression** [!INCLUDE[mapop](/Token/mapop_md.md)]. Connect the **UnitPrice** and **Quantity** elements from the source schema to this [!INCLUDE[mapop](/Token/mapop_md.md)]. Double-click the [!INCLUDE[mapop](/Token/mapop_md.md)] to open the **Configure Arithmetic Expression** dialog box, and in the **Enter arithmetic expression** box, type **UnitPrice &#42; Quantity**.

7. By now, we have calculated the value of **UnitPrice &#42; Quantity** for each iteration of the **OrderDetails** element. We now need to assign this value to the **Amount** variable we created as part of the **List** operation. To do so, we include an **Add Item to List** operation within the **ForEach Loop** operation and connect it to the **Arithmetic Expression** operation. Doing this assigns the value from the **Arithmetic Expression**[!INCLUDE[mapop](/Token/mapop_md.md)] (which is **Unit Price &#42; Quantity**) to the **Amount** variable created as part of the **List** operation.

8. A List operation could have many variables defined. Even though in our tutorial, we have just one variable (**Amount**) defined, we still need to configure the [!INCLUDE[transform](/Token/transform_md.md)] to pick that variable. To do so, we use the **Select Entries**[!INCLUDE[mapop](/Token/mapop_md.md)].

   Drag and drop the **Select Entries**[!INCLUDE[mapop](/Token/mapop_md.md)] to the design surface and connect it to the **Create List** operation. Double-click the **Select Entries**[!INCLUDE[mapop](/Token/mapop_md.md)] to open the **Configure Select Entries** dialog box, and from the **Select members** box, select the check box against **Amount**.

9. We now need to do a cumulative sum of the value in the Amount variable. So, we add a Cumulative Sum [!INCLUDE[mapop](/Token/mapop_md.md)] and then connect it to the Select Entries [!INCLUDE[mapop](/Token/mapop_md.md)]. Double-click the Cumulative Sum [!INCLUDE[mapop](/Token/mapop_md.md)] and in the text box, enter the following expression:

   ```
   item.Amount
   ```
   We must now connect the **Cumulative Sum**[!INCLUDE[mapop](/Token/mapop_md.md)] to the **TotalAmount** element in the destination schema. This is how the [!INCLUDE[transform](/Token/transform_md.md)] should resemble (only for mapping the TotalAmount element in the destination schema):

   ![](/Image/AFINT_FTPTut_AmountMap.gif)

   > [!NOTE]
   > You can also look at the map available as part of the **FTP_EAI_Tutorial** sample available at [http://go.microsoft.com/fwlink/?LinkId=247973](http://go.microsoft.com/fwlink/?LinkId=247973).

## See Also
[Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server](/Topic/Tutorial__Using_BizTalk_Bridges_to_Insert_Flat_File_Messages_into_an_On-premises_SQL_Server.md)

