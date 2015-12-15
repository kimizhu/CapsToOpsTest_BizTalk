---
description: na
keywords: na
pagetitle: You can Build and deploy the BizTalk Services project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0aff562-98bb-4f1e-babb-47154fa3b7e7
---
# You can Build and deploy the BizTalk Services project
In this topic we connect the [!INCLUDE[one-way](/Token/one-way_md.md)] to [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob and then build the [!INCLUDE[af_integration](/Token/af_integration_md.md)] project.

### To connect the components and build the project

1. Select **Connector** from the **Toolbox** on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] designer surface then connect the **PurchaseOrderBridge** with **PO_Blob**.

   ![](/Image/WABS_CloudCar_POBridge.PNG)

2. Select the connection between the bridge and the blob, then select the **Filter Condition** property from the Properties pane.

3. In the **Route Filter Configuration** dialog box, select **Match All**. This ensures that all the messages that are processed by the bridge are routed to the blob.

4. Right-click the **CloudCar_Integration_PurchaseOrder** project, and then select **Build**.

5. Once the build succeeds, right-click the project then select **Deploy**.

6. In the deployment window, the **Deployment Endpoint** is a read only entity and the value is derived from the **BizTalk Service URL/Namespace** set in the message flow surface. However, you must provide the ACS Namespace for [!INCLUDE[af_integration](/Token/af_integration_md.md)], Issuer Name, and Shared Secret.

7. Select **Deploy**. The [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] Output pane displays the deployment progress and result. The URL where the [!INCLUDE[bridge](/Token/bridge_md.md)] is deployed is also displayed in the Output pane.

## See Also
[Create a BizTalk Service project to process purchase orders](/Topic/Create_a_BizTalk_Service_project_to_process_purchase_orders.md)

