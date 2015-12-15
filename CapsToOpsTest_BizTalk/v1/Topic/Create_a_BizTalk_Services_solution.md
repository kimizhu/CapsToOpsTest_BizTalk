---
description: na
keywords: na
pagetitle: Create a BizTalk Services solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3a6b8d2-a9fb-4b08-a2cc-879446655920
---
# Create a BizTalk Services solution
In this section, we create a [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] solution that contains two [!INCLUDE[af_integration](/Token/af_integration_md.md)] projects, **CloudCar_Integration_PurchaseOrder** and **CloudCar_Integration_Invoice**. The **CloudCar_Integration_PurchaseOrder** project receives purchase order messages from the customer, converts them to X12 850 purchase order message and routes it to the **purchaseorder** blob container. The **CloudCar_Integration_Invoice** project receives X12 810 invoice messages from Fourth Coffee, converts them to the invoice message schema expected by Contoso, Ltd. and routes it to the **invoice** blob container.

> [!NOTE]
> If you want to use the sample [!INCLUDE[af_integration](/Token/af_integration_md.md)] project instead, you can download it from the MSDN code gallery at [http://go.microsoft.com/fwlink/p/?LinkId=390148](http://go.microsoft.com/fwlink/p/?LinkId=390148).

## In This Section

- [Create a BizTalk Service project to process purchase orders](/Topic/Create_a_BizTalk_Service_project_to_process_purchase_orders.md)

- [Create a BizTalk Service project to process invoices](/Topic/Create_a_BizTalk_Service_project_to_process_invoices.md)

## See Also
[Set up the integration layer](/Topic/Set_up_the_integration_layer.md)

