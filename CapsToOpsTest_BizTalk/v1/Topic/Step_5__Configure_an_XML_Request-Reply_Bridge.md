---
description: na
keywords: na
pagetitle: Step 5: Configure an XML Request-Reply Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d454ae2-0414-44c0-892e-efaf8e8c8e5b
---
# Step 5: Configure an XML Request-Reply Bridge
Lists the steps to configure an [!INCLUDE[request_response](/Token/request_response_md.md)]. The bridge receives XML sales order messages sent from Contoso. To configure a bridge for the scenario in this tutorial, you must:

- The bridge must validate all incoming XML messages against the **ECommerceSalesOrder.xsd** schema. This is the schema in which Northwind expects Contoso to send sales order messages.

- The bridge must transform the message in **ECommerceSalesOrder** schema to the schema for inserting data into the **SalesOrder** SQL Server table. To do so, the bridge must use the **SalesOrder_SQL**[!INCLUDE[transform](/Token/transform_md.md)].

- The bridge must route the message to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] endpoint. While routing the message, the bridge must also include the relevant headers that must be added to successfully insert messages into the **SalesOrder** table.

This topic lists the steps to achieve these tasks as part of a [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

### To configure the [!INCLUDE[request_response](/Token/request_response_md.md)]

1. Double click on the .bcs file in the **EAIEDITutorial** project to open the message flow.

2. Right-click anywhere on the design area and select **Properties**. In the **BizTalk Service URL** property, verify that you have the [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL entered. This is the name that you entered in [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414) when creating the [!INCLUDE[af_integration](/Token/af_integration_md.md)].

3. Right click the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] (added in [Step 3: Create and Configure LOB Targets](/Topic/Step_3__Create_and_Configure_LOB_Targets.md)) and select **Properties**. Under **Operations** tab, copy the value of the first operation and save it to a notepad. This value is used later. For this tutorial, the value is `TableOp/Insert/dbo/SalesOrder`.

4. Drag and drop an [!INCLUDE[request_response](/Token/request_response_md.md)] from toolbox to the message flow area. You use a [!INCLUDE[request_response](/Token/request_response_md.md)] to send the response back to the client that the sales order data is inserted successfully in the **SalesOrder** table.

5. Configure the [!INCLUDE[request_response](/Token/request_response_md.md)]:

   1. Double-click the [!INCLUDE[request_response](/Token/request_response_md.md)] on the message flow area.

   2. Add the request and response schemas to the **Message Type** box:

      |||
      |-|-|
      |Request schema <br /> <br />|SalesOrder (with the namespace `http://ECommerceSalesOrder.Inbound`) <br /> <br />|
      |Response schema <br /> <br />|InsertResponse <br /> <br />|
      To add request and response schemas, see [Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md).

   3. Add the **SalesOrder_SQL** transform to the [!INCLUDE[transform](/Token/transform_md.md)]s stage in the request path of the [!INCLUDE[bridge](/Token/bridge_md.md)]. Select the **XmlTransform** activity under [!INCLUDE[transform](/Token/transform_md.md)] stage. In Properties, select the ellipsis **(…)** button next to the **Maps** property. In **Maps Selection**, select **SalesOrder_SQL.trfm**[!INCLUDE[transform](/Token/transform_md.md)] and select **OK**. The selected map is now reflected in the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

   4. Leave everything else in the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration to its default value.

6. Go back to the message flow area (MessageFlowItinerary.bcs). Select the **Connector** in the toolbox and join the [!INCLUDE[request_response](/Token/request_response_md.md)] and **orderprocessing_sqlgetorder** entity.

7. Set the filter condition on the connector between the [!INCLUDE[bridge](/Token/bridge_md.md)] and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] entity. The business process between Contoso and Northwind does not include any condition, like only specific messages must be inserted into the **SalesOrder** table. Hence, the filter condition must allow all messages to go through.

   1. Select the connector between [!INCLUDE[request_response](/Token/request_response_md.md)] and the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] entity.

   2. In **Properties**, select the ellipsis **(…)** button for **Filter Condition**.

   3. In **Route Filter Configuration**, set the filter condition to **Match All**.

   4. Select **OK**.

8. To insert data into the **SalesOrder** table using the XML message, the message header must include the **Action** SOAP header. You can set headers on the messages being sent from a [!INCLUDE[bridge](/Token/bridge_md.md)] using the Route action property, which is available on the connector between the [!INCLUDE[bridge](/Token/bridge_md.md)] and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)].

   1. On the message flow area, select the connector between [!INCLUDE[request_response](/Token/request_response_md.md)] and the **orderprocessing_sqlgetorder** entity.

   2. In **Properties**, select the ellipsis **(…)** button for **Route Action**. In **Route Actions**, select **Add** to open the **Add Route Action** dialog box. In **Add Route Action**, set the properties as shown in the following table:

      **Under Property (Read From)**

      |||
      |-|-|
      |Expression <br /> <br />|Set this to `TableOp/Insert/dbo/SalesOrder` **Important:** Always enter the value for an expression within single quotes. <br />|
      **Under Destination (Write-To)**

      |||
      |-|-|
      |Type <br /> <br />|Set this to SOAP. <br /> <br />|
      |Identifier <br /> <br />|Set this to Action. <br /> <br />|
      With this configuration, when the [!INCLUDE[bridge](/Token/bridge_md.md)] routes the message to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)], the message includes an **Action** header and the value of the header is set to *TableOp/Insert/dbo/SalesOrder*; which is the action required to insert a message in the **SalesOrder** table.

   3. Select **OK** in the **Add Route Action** and the **Route Actions** windows. Select **Save** to save changes to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

## See Also
[Create and Deploy the BizTalk Services Project](/Topic/Create_and_Deploy_the_BizTalk_Services_Project.md)

