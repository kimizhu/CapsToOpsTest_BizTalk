---
description: na
keywords: na
pagetitle: Create a BizTalk Service project to process purchase orders
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81722b9a-3958-4687-b6cc-d14be2d9d251
---
# Create a BizTalk Service project to process purchase orders
The topics in this section demonstrate how to create the **CloudCar_Integration_PurchaseOrder**[!INCLUDE[af_integration](/Token/af_integration_md.md)] project. The [!INCLUDE[af_integration](/Token/af_integration_md.md)] project includes the following components:

- An [!INCLUDE[one-way](/Token/one-way_md.md)] in the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

- An [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob destination.

- A SQL Server [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to insert purchase order data into a SQL Server database.

- Custom code component within the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], which uses the SQL Server [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to write data to the SQL Server database.

Finally, you connect the components, build the project, and deploy it.

## In This Section

- [Add an XML one-way bridge to process purchase order](/Topic/Add_an_XML_one-way_bridge_to_process_purchase_order.md)

- [Add an Azure blob destination to receive purchase order](/Topic/Add_an_Azure_blob_destination_to_receive_purchase_order.md)

- [Create a SQL Server LOB target to insert purchase order](/Topic/Create_a_SQL_Server_LOB_target_to_insert_purchase_order.md)

- [Include custom code to insert purchase order into SQL Server](/Topic/Include_custom_code_to_insert_purchase_order_into_SQL_Server.md)

- [You can Build and deploy the BizTalk Services project](/Topic/You_can_Build_and_deploy_the_BizTalk_Services_project.md)

## See Also
[Create a BizTalk Services solution](/Topic/Create_a_BizTalk_Services_solution.md)

