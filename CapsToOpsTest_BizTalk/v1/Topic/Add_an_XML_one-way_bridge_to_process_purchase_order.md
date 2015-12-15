---
description: na
keywords: na
pagetitle: Add an XML one-way bridge to process purchase order
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a2d6392-c18b-4535-9119-1a2bc878de9b
---
# Add an XML one-way bridge to process purchase order
This topic provides instructions on how to create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and how to add an [!INCLUDE[one-way](/Token/one-way_md.md)] to it. The [!INCLUDE[one-way](/Token/one-way_md.md)] receives the customer orders and transforms it an X12 850 purchase order. The bridge also invokes a custom code component that inserts the purchase order data (before it is transformed to X12 850 purchase order) into a SQL Server database. Instructions related to creating the custom code component and including it in the bridge configuration is available at [Include custom code to insert purchase order into SQL Server](/Topic/Include_custom_code_to_insert_purchase_order_into_SQL_Server.md).

### To add an XML one-way bridge

1. Open Visual Studio (as an administrator), create a new [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], and name it **CloudCar_Integration_PurchaseOrder**. Name the solution as **ClouCar_Integration**.

2. In the **CloudCar_Integration_PurchaseOrder** project, from the Solution Explorer, double-click the **MessageFlowItinerary.bcs** file to open the bridge configuration surface.

3. Right-click anywhere on [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface, select **Properties**, and update the **BizTalk Service URL** property to include your [!INCLUDE[af_integration](/Token/af_integration_md.md)] name. This is the name that you provided in the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414) while provisioning [!INCLUDE[af_integration](/Token/af_integration_md.md)].

4. From the **Toolbox**, drag and drop the **[!INCLUDE[one-way](/Token/one-way_md.md)]** component to the bridge design surface.

5. Right-click the **[!INCLUDE[one-way](/Token/one-way_md.md)]**, select **Properties**, and change the value for **Entity Name** and **Relative Address** properties to **PurchaseOrderBridge**. As a result, the complete endpoint URL where the bridge is deployed, which is shown in the **Runtime Address** property, will resemble `https://*<mybiztalkservicename>*.biztalk.windows.net/default/PurchaseOrderBridge`. This endpoint receives the customer order message from the car.

6. Add the following artifacts to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and save the changes.

   |Artifact name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |CustomerOrder.xsd <br /> <br />|Message schema in which the customer order is received <br /> <br />|
   |X12_00401_850.xsd <br /> <br />|Message schema for X12 850 purchase order message <br /> <br />|
   |CustomerOrderTo850.trfm <br /> <br />|Transforms CustomerOrder.xsd to X12 850 schema <br /> <br />|
   You can download these artifacts, which are included with the sample, uploaded to the MSDN code gallery at [http://go.microsoft.com/fwlink/p/?LinkId=324220](http://go.microsoft.com/fwlink/p/?LinkId=324220).

7. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] to open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface and enter the message type that is processed by the [!INCLUDE[bridge](/Token/bridge_md.md)]. To enter the message type, within the **Message Types** box, select the add icon [ ![](/Image/IntSvcs_Bridges_Add_Icon.gif) ] to open the **Message Type Picker** dialog box.

8. In the **Message Type Picker** dialog box, from the **Available message types** box, select the schema for the request message and then select the right arrow icon  [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ], and then select **OK**. For this tutorial, select the **CustomerOrder.xsd** schema (`http://CloudCar.CustomerOrder#CustomerOrder`). The selected schema should now be listed under the **Request Message Type** box.

9. Within the **Transform** stage, select the **Xml Transform** activity, and then from the **Properties** pane, select the ellipsis against the **Map** property. In the **Map Selection** dialog box, select the **CustomerOrderTo850.trfm** to add it to the bridge configuration.

10. Save changes to the project.

## See Also
[Create a BizTalk Service project to process purchase orders](/Topic/Create_a_BizTalk_Service_project_to_process_purchase_orders.md)

