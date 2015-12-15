---
description: na
keywords: na
pagetitle: Step 6: Configure an XML One-Way Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3922cd4d-42fa-4ff3-83de-8d95b1ce8826
---
# Step 6: Configure an XML One-Way Bridge
This topic provides instructions on how to configure an [!INCLUDE[one-way](/Token/one-way_md.md)]. As part of the [!INCLUDE[one-way](/Token/one-way_md.md)] configuration, we’ll do the following:

- Configure the [!INCLUDE[bridge](/Token/bridge_md.md)] to process the flat-file message of the type we created earlier.

- Through promoted properties, extract the value of the **OrderId** record (before message transformation) and **TotalAmount** (after message transformation). We’ll track the values for these two as the message gets processed by the [!INCLUDE[bridge](/Token/bridge_md.md)].

- Configure the [!INCLUDE[bridge](/Token/bridge_md.md)] to use the **Map.trfm**[!INCLUDE[transform](/Token/transform_md.md)] we created earlier.

- Configure the [!INCLUDE[bridge](/Token/bridge_md.md)] to track the messages it processes.

### To configure an [!INCLUDE[one-way](/Token/one-way_md.md)]

1. Drag and drop an [!INCLUDE[one-way](/Token/one-way_md.md)] from toolbox to the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design area. For the Entity Name and Relative Address properties of the bridge, enter **ProcessOrders** for the value.

2. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] on the itinerary designer.

3. On the [!INCLUDE[one-way](/Token/one-way_md.md)] design area, within the **Message Types** box, select the add icon [ ![](/Image/IntSvcs_Bridges_Add_Icon.gif) ] to open the **Message Type Picker** dialog box.

4. In the **Message Type Picker** dialog box, from the **Available message types** box, select the **PurchaseOrder** message type, select the right arrow icon  [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ] to associate the request schema with the [!INCLUDE[one-way](/Token/one-way_md.md)], and then click **OK**. The schema that you selected should now be listed under the **Request Message Type** section.

5. Configure the pre-transform **Enrich** stage to extract the value of the **OrderId** element in the source schema.

   1. Within the **Enrich** stage, select the **Enrich** activity, and then from the **Properties** pane, select the ellipsis button **(…)** against the **Properties** property to open the **Property Definition** dialog box.

   2. In **Property Definitions**, select **Add** to open the **Add Property** dialog box. In the **Add Property** dialog box, do the following:

      |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
      |-----------|--------------|---------------|
      |Source (Read From) <br /> <br />|Type <br /> <br />|Select **Xpath** from the drop-down list. <br /> <br />|
      |Source (Read From) <br /> <br />|Identifier <br /> <br />|Specify the Xpath query to extract the value of the **OrderId** from the request schema. **Tip:** You can get the Xpath query from the schema editor. Select the **OrderId** element in the schema editor, and in the Properties window look for the value of the **Instance Xpath** property. That should be the Xpath query for the node. <br />|
      |Source (Read From) <br /> <br />|Message Type <br /> <br />|Select the schema pertaining to **PurchaseOrder**. <br /> <br />|
      |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specifies the name of the property that you are defining. For this tutorial, specify **OrderId**. <br /> <br />|
      |Property (Write To) <br /> <br />|Data Type <br /> <br />|Specifies the data type for the property. For this tutorial, specify **string**. <br /> <br />|

   3. Select **OK** in the **Add Property** dialog box and then select **OK** in the **Property Definition** dialog box.

6. Configure the [!INCLUDE[bridge](/Token/bridge_md.md)] to use the [!INCLUDE[transform](/Token/transform_md.md)] created earlier. Within the **[!INCLUDE[transform](/Token/transform_md.md)]** stage, select the **Xml Transform** activity, and then from the **Properties** window, select the ellipsis button **(…)** against the **Maps** property to open the **Map Selection** dialog box.

   From the list of [!INCLUDE[transform](/Token/transform_md.md)]s displayed in the dialog box, select **Map.trfm**. You created this [!INCLUDE[transform](/Token/transform_md.md)] in the previous steps.

7. Configure the post-transform **Enrich** stage to extract the value of the **TotalAmount** element in the source schema.

   1. Within the **Enrich** stage, select the **Enrich** activity, and then from the **Properties** pane, select the ellipsis button **(…)** against the **Properties** property to open the **Property Definition** dialog box.

   2. In the **Property Definitions** dialog box, select **Add** to open the **Add Property** dialog box. In the **Add Property** dialog box, do the following:

      |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
      |-----------|--------------|---------------|
      |Source (Read From) <br /> <br />|Type <br /> <br />|Select **Xpath** from the drop-down list. <br /> <br />|
      |Source (Read From) <br /> <br />|Identifier <br /> <br />|Specify the Xpath query to extract the value of the **TotalAmount** from the request schema. <br /> <br />|
      |Source (Read From) <br /> <br />|Message Type <br /> <br />|Select the schema pertaining to **Insert**. <br /> <br />|
      |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specifies the name of the property that you are defining. For this tutorial, specify **TotalAmount**. <br /> <br />|
      |Property (Write To) <br /> <br />|Data Type <br /> <br />|Specifies the data type for the property. Specify **long**. <br /> <br />|

   3. Select **OK** in the **Add Property** dialog box and then select **OK** in the **Property Definition** dialog box.

   4. Save changes to the project.

8. Configure the [!INCLUDE[bridge](/Token/bridge_md.md)] to track message properties and other data, for the **OrderId** and **TotalAmount** properties you just promoted.

   1. Go back to the MessageFlowItinerary.bcs file, select the [!INCLUDE[one-way](/Token/one-way_md.md)], and from the **Properties** window, select the ellipsis (…) against **Track Properties**.

   2. Select the **Track message processing events** check box to track detailed information such as when a stage starts, completes, or faults; when an activity within a stage starts, completes, or faults; whether an artifact gets retrieved, etc.

   3. Optional. Select the **Track all message properties** check box, and then select the properties you want to track. Note that the dialog box lists the properties that you promoted within any of the **Enrich** stages in a bridge.

      For this tutorial, select **OrderId** and **TotalAmount**.

   4. Select **OK**.

9. Save the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration and go back to the [!INCLUDE[msgflow](/Token/msgflow_md.md)] designer area.

10. Connect the FTP source component to the [!INCLUDE[one-way](/Token/one-way_md.md)] and the [!INCLUDE[bridge](/Token/bridge_md.md)] to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] entity.

11. Set the filter condition on the connector between the [!INCLUDE[bridge](/Token/bridge_md.md)] and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] entity.

   1. Select the connector between [!INCLUDE[one-way](/Token/one-way_md.md)] and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] entity.

   2. In the **Properties** window, select the ellipsis **(…)** button for **Filter Condition**.

   3. In the **Route Filter Configuration** dialog box, set the filter condition to **Match All**.

   4. Select **OK**.

12. Set the Route action so that the outgoing message to the LOB application has a SOAP action header.

   1. Open **Server Explorer** and navigate to the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)][!INCLUDE[lobrelay](/Token/lobrelay_md.md)] we created earlier. Right click the relay, select **Properties**, and for the **Operations** property, copy the value of the first operation.

   2. On the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design area, click the connector between [!INCLUDE[one-way](/Token/one-way_md.md)] and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] entity.

   3. In **Properties**, select the ellipsis **(…)** button for **Route Action**. In **Route Actions**, select **Add** to open the **Add Route Action** dialog box. In the **Add Route Action** dialog box, do the following:

   4. Under **Property (Read From)** section, select **Expression**, and then paste the value that you copied.

      > [!IMPORTANT]
      > You must always specify the value for an expression within single quotes.

   5. Under **Destination (Write To)** section, set the Type to **SOAP** and the **Identifier** to **Action**.

      > [!IMPORTANT]
      > You must always specify the value for an expression within single quotes.

   6. Select **OK** in the **Add Route Action** dialog box to add the route action. Select **OK** in the **Route Actions** dialog box and then select **Save** to save changes to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

## See Also
[Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server](/Topic/Tutorial__Using_BizTalk_Bridges_to_Insert_Flat_File_Messages_into_an_On-premises_SQL_Server.md)

