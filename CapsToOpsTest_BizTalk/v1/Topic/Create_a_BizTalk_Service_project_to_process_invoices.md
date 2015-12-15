---
description: na
keywords: na
pagetitle: Create a BizTalk Service project to process invoices
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8ebf10b-d76d-4885-9f4a-fbe8e2ebe8ac
---
# Create a BizTalk Service project to process invoices
The topics in this section demonstrate how to create the **CloudCar_Integration_Invoice**[!INCLUDE[af_integration](/Token/af_integration_md.md)] project. The [!INCLUDE[af_integration](/Token/af_integration_md.md)] project includes the following components:

- An [!INCLUDE[one-way](/Token/one-way_md.md)] in the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

- An [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob destination.

- A SQL Server [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to insert invoice data into a SQL Server database.

- Custom code component within the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], which uses the SQL Server [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to write data to the SQL Server database and send an e-mail with the invoice details to the customer.

Finally, you connect the components, build the project, and deploy it.

## In This Section

- [Add an XML one-way bridge to process invoice](/Topic/Add_an_XML_one-way_bridge_to_process_invoice.md)

- [Add an Azure blob destination to receive invoice](/Topic/Add_an_Azure_blob_destination_to_receive_invoice.md)

- [Create a SQL Server LOB target to insert invoice](/Topic/Create_a_SQL_Server_LOB_target_to_insert_invoice.md)

- [Include custom code to insert invoice into SQL Server](/Topic/Include_custom_code_to_insert_invoice_into_SQL_Server.md)

- [Build and deploy the BizTalk Services project](/Topic/Build_and_deploy_the_BizTalk_Services_project.md)

## See Also
[Create a BizTalk Services solution](/Topic/Create_a_BizTalk_Services_solution.md)

