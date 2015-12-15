---
description: na
keywords: na
pagetitle: Add an XML one-way bridge to process invoice
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 659f4c4b-3b42-41b9-98b8-51592e71f397
---
# Add an XML one-way bridge to process invoice
This topic provides instructions on how to create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and how to add an [!INCLUDE[one-way](/Token/one-way_md.md)] to it. The [!INCLUDE[one-way](/Token/one-way_md.md)] receives the X12 810 invoice message from the EDI receive bridge and transforms it to a schema in which Contoso, Ltd. expects the invoice messages. The bridge also invokes a custom code component that inserts the invoice data (after it is transformed to Contoso, Ltd.’s invoice schema) into a SQL Server database. Instructions related to creating the custom code component and including it in bridge configuration is available at [Include custom code to insert invoice into SQL Server](/Topic/Include_custom_code_to_insert_invoice_into_SQL_Server.md).

### To add an XML one-way bridge

1. Within the **CloudCar_Integration** solution, add a new [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], and name it **CloudCar_Integration_Invoice**.

2. In the **CloudCar_Integration_Invoice** project, from the Solution Explorer, double-click the **MessageFlowItinerary.bcs** file to open the bridge configuration surface.

3. Right-click anywhere on [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface, select **Properties**, and update the **BizTalk Service URL** property to include your [!INCLUDE[af_integration](/Token/af_integration_md.md)] name. This is the name that you provided in the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414) while provisioning [!INCLUDE[af_integration](/Token/af_integration_md.md)].

4. From the **Toolbox**, drag and drop the **[!INCLUDE[one-way](/Token/one-way_md.md)]** component to the bridge design surface.

5. Right-click the **[!INCLUDE[one-way](/Token/one-way_md.md)]**, select **Properties**, and change the value for **Entity Name** and **Relative Address** properties to **InvoiceBridge**. As a result, the complete endpoint URL where the bridge is deployed, which is shown in the **Runtime Address** property, will resemble `https://*<mybiztalkservicename>*.biztalk.windows.net/default/InvoiceBridge`. This endpoint receives the X12 810 invoice from the EDI Receive bridge.

6. Add the following artifacts to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and save the changes.

   |Artifact name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |Invoice.xsd <br /> <br />|Message schema in which the invoice is expected <br /> <br />|
   |X12_00401_850.xsd <br /> <br />|Message schema for X12 810 invoice message <br /> <br />|
   |810ToInvoice.trfm <br /> <br />|Transforms X12 810 invoice to Invoice.xsd. <br /> <br />|
   You can download these artifacts, which are included with the sample, uploaded to the MSDN code gallery at [http://go.microsoft.com/fwlink/p/?LinkId=324220](http://go.microsoft.com/fwlink/p/?LinkId=324220).

7. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] to open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface and enter the message type that is processed by the [!INCLUDE[bridge](/Token/bridge_md.md)]. To specify the message type, within the **Message Types** box, select the add icon [ ![](/Image/IntSvcs_Bridges_Add_Icon.gif) ] to open the **Message Type Picker** dialog box.

8. In the **Message Type Picker** dialog box, from the **Available message types** box, select the schema for the request message and then select the right arrow icon  [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ], and then select **OK**. For this tutorial, select the **X12_00401_810.xsd** schema because messages with this schema are routed to the [!INCLUDE[bridge](/Token/bridge_md.md)]. The selected schema should now be listed under the **Request Message Type** box.

9. Within the **Transform** stage, select the **Xml Transform** activity, and then from the **Properties** pane, select the ellipsis against the **Map** property. In the **Map Selection** dialog box, select the **810ToInvoice.trfm** to add it to the bridge configuration.

10. Save changes to the project.

## See Also
[Create a BizTalk Service project to process invoices](/Topic/Create_a_BizTalk_Service_project_to_process_invoices.md)

