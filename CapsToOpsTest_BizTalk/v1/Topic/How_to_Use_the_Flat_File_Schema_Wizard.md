---
description: na
keywords: na
pagetitle: How to Use the Flat File Schema Wizard
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33b5de1f-1e4f-4f98-a39e-c2ebaeb23d1d
---
# How to Use the Flat File Schema Wizard
This walkthrough shows you how to create a flat file schema from a document instance using the Flat File Schema Wizard based on the following sample purchase order:

![](/Image/AFINT_FF_POSchema.gif)

Each line of the purchase order ends with a carriage return line feed (CRLF), marked in green. The purchase order starts with a PO tag shown in red and followed by a date. Two repeating fixed positional fields contain customer information and are shown in purple. After the comment field, there is a repeating field starting with an ITEMS tag that contains multiple records delimited by commas (,) and data values separated by pipes (|), which are shown in blue.

## Prerequisites
To prepare the document instance for the walkthrough, copy the following to notepad and save it as a text file:

```
PO1999-10-20US        Alice Smith         123 Maple Street    Mill Valley    CA 90952US        Robert Smith        8 Oak Avenue        Old Town       PA 95819ITEMS,ITEM872-AA|Lawnmower|1|148.95|Confirm this is electric,ITEM926-AA|Baby Monitor|1|39.98|Confirm this is electric
```

### To use the Flat File Schema wizard

1. In Visual Studio, create a new BizTalk Service Project. See [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. To add the new flat file schema, right-click the project, and click **Add**, and then click **New Item**.

3. In the **Add New Item** dialog box, select **Generate Flat File Schema**, enter a name for the schema, and then click **Add**. The Flat File Schema Wizard starts.

4. On the **Flat File Schema Information** screen, select your instance and enter the following information. When you are done, click **Next** to continue.

   1. **Instance file:** Click the **Browse** button to locate the flat file from which the schema will be generated. Browse to the folder containing the text file you created in the Prerequisites section.

   2. **Record name:** Type **PO** as it will be the schema root name.

   3. **Target namespace:** Type **http://EnterpriseApplicationIntegration.PurchaseOrder** for schema target namespace.

5. On the **Select Document Data** screen, the contents of the flat file are displayed. Select the data needed for creating the schema, and then click **Next**. In this walkthrough, because we are using the entire document instance, you can press **Ctrl-A** to select all.

6. In the **Select Record Format** screen, you specify whether the records are formatted using a delimiter symbol or by defining relative positions. In the instance message we chose, the purchase order records end with a carriage return line feed (CRLF), hence select **By delimiter symbol**, and then click **Next**.

7. On the **Delimited Record** screen, enter the following to define the first level of the schema and when you are done, click **Next**.

   1. **Child delimiter:** Select **{CR}{LF}**.

      > [!NOTE]
      > **Child delimiter** property is an editable box with drop down selection list contains a set of default values. The **Child delimiter** can be specified as a character or as a hexadecimal value. For example, **\{** or **{0x0D0A}**.

   2. **Escape character:** An escape character is a single character that suppresses any special meaning of the character that follows it. See [Escape Characters](http://go.microsoft.com/fwlink/?LinkId=245838) for more information. For this walkthrough, leave this blank.

      > [!NOTE]
      > When using **\**, **{,** and **}** for **Child delimiter** or **Escape character**, a back slash must be used. For example, **\\,** and **\{**.

   3. Check **Record has a tag identifier** box and type **PO** in the **Tag** text box. If there are more than one flat file message types being processed by the bridge, this tag is used to identify which flat-file schema to validate the incoming message against.

   4. Click **Next** to continue.

   ![](/Image/AFINT_FF_PO_delimiter.gif)

8. The wizard identifies four elements in the purchase order record; you must now define the element property. Make changes as illustrated in the following table:

   |Element Name <br /> <br />|Element Type <br /> <br />|Data Type <br /> <br />|
   |----------------|----------------|-------------|
   |Enter **date** <br /> <br />|Select **Field Element**. <br /> <br />|Select **date** <br /> <br />|
   |Enter **customer** <br /> <br />|Select **Repeating record** <br /> <br />|- <br /> <br />|
   ||Select **Ignore** **Note:** You set this to **Ignore** because you have already specified **Repeating Record** for the **customer** element. <br />|- <br /> <br />|
   |Enter **items** <br /> <br />|Select **Record** <br /> <br />|- <br /> <br />|
   ![](/Image/AFINT_FF_PO.gif)

   > [!NOTE]
   > You can select multiple rows and then change their **Element Type** to a single type by using the mouse and the SHIFT or CTRL key.

   > [!NOTE]
   > After you click **Next** on the **Child Elements** screen, you will not be able to click **Back** to redefine or make any changes to the child elements. You may need to close the wizard and launch the wizard again to define the flat file schema.

9. After you complete the steps until here, the first level of the schema is generated as shown in the **Schema View** page. Three unique elements are defined, and you will continue to further define the child records for the elements in the purchase order record.

   ![](/Image/AFINT_FF_POSc.gif)

   Because we defined the **customer** element as the **Repeating record** type and the **items** element as the **Record** type, the Flat File Schema Wizard now continues to further define these two elements. On the **Schema View** page, select **customer**, and then click **Next** to continue.

10. To work with the customer record, you need to select the data that represents that element. Because it is a repeating record, either of the lines can be used to define the record. Select the first line of customer data and click **Next** to continue.

11. On the **Select Record Format** page, select **By relative positions**, and then click **Next**.

12. The wizard provides a visual tool for showing and calculating the distance between the fields. On the **Positional Record** page, use the left mouse button to click the position marker to represent where the name field begins. Click the following position markers to represent the rest of the data fields:

   |Field Name <br /> <br />|Position Marker <br /> <br />|
   |--------------|-------------------|
   |**name** <br /> <br />|10 <br /> <br />|
   |**street** <br /> <br />|30 <br /> <br />|
   |**city** <br /> <br />|50 <br /> <br />|
   |**state** <br /> <br />|65 <br /> <br />|
   |**postalcode** <br /> <br />|68 <br /> <br />|
   ![](/Image/AFINT_FF_Cust.gif)

   Click **Next** to continue.

13. On the **Child Elements** page, you specify the properties of the child elements. Select the row and type names for the elements under the **Element Name**. Leave the default values in the other columns. Type the following values for the properties listed in the **Element Name** column:

   |For Element Name <br /> <br />|Enter Value <br /> <br />|
   |--------------------|---------------|
   |**customer_Child1** <br /> <br />|**country** <br /> <br />|
   |**customer_Child2** <br /> <br />|**fullName** <br /> <br />|
   |**customer_Child3** <br /> <br />|**street** <br /> <br />|
   |**customer_Child4** <br /> <br />|**city** <br /> <br />|
   |**customer_Child5** <br /> <br />|**state** <br /> <br />|
   |**customer_Child6** <br /> <br />|**postalcode** <br /> <br />|
   ![](/Image/AFINT_FF_Cust_.gif)

14. The child elements of the customer record are created as shown in the following screenshot of the **Schema View** page. Click **Next** to define the child elements for the items record.

   ![](/Image/AFINT_FF_CustSchemaView.gif)

   On the **Schema View** page, select **items**, and then click **Next**.

15. On the **Select Document Data** page, select the entire line beginning with ITEMS, and then click **Next** to define its child elements.

16. On the **Select Record Format** page, select **By delimiter symbol**, and then click **Next**.

17. In the Items record, commas are used to delimit the individual items. Therefore, on the **Delimited Record** page, enter the following to define the items record. When you are done, click **Next**.

   1. Select **,** from **Child delimiter** drop-down selection list.

   2. Leave the **Escape character** text box blank.

   3. Select **Record has a tag identifier** and type **ITEMS** in the **Tag** text box. In case of multiple items record, **ITEMS** is used to identify each individual record.

   ![](/Image/AFINT_FF_ItemsDelimiter.gif)

18. Using the values from the **Delimited Record** page, the wizard identifies two child elements. Because one of them is a repeating record, select the first element and enter **item** for Element Name, and then select **Repeating Record** from the drop down selection list for **Element Type**. Leave the rest of the default values in the columns.

   Select the second row and select the **Ignore** from **Element Type** list.

   ![](/Image/AFINT_FF_ItemsElement.gif)

   When you click **Next**, the next level for the items record is created in the schema.

   ![](/Image/AFINT_FF_ItemsSchView.gif)

   You continue to define the final part of the purchase order schema. On the Schema View page, select **item** and then click **Next** to continue.

19. On the **Select Document Data** page, select **ITEM872-AA|Lawnmower|1|148.95|Confirm this is electric**. Click **Next** to continue.

20. On the **Select Record Format** page, select the **By delimiter symbol** option because the individual item is delimited by a pipe (|).

21. On the **Delimited Record** page, enter the following to define the item record. When you are done, click **Next**.

   - Select **|** from the **Child delimiter** drop down selection list.

   - Leave the **Escape character** text box blank.

   ![](/Image/AFINT_FF_ItemDelimiter.gif)

22. On the **Child Elements** page, the wizard has identified five child elements. Select the row and enter values for **Element name** properties, as shown in the table below. Leave the default values in the rest of the columns.

   |For Element Name <br /> <br />|Enter Value <br /> <br />|
   |--------------------|---------------|
   |**item_Child1** <br /> <br />|**productCode** <br /> <br />|
   |**item_Child2** <br /> <br />|**description** <br /> <br />|
   |**item_Child3** <br /> <br />|**quantity** <br /> <br />|
   |**item_Child4** <br /> <br />|**unitPrice** <br /> <br />|
   |**item_Child5** <br /> <br />|**notes** <br /> <br />|
   ![](/Image/AFINT_FF_ItemElements.gif)

   Click **Next**.

23. You have defined all the nodes for the purchase order schema. On the **Schema View** page, click **Finish**.

