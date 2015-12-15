---
description: na
keywords: na
pagetitle: Step 7: Build and Deploy the Project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea527592-578d-4aa3-a0d9-2f27a5753231
---
# Step 7: Build and Deploy the Project
This topic lists the steps to build and deploy the [!INCLUDE[af_integration](/Token/af_integration_md.md)] solution.

### To build and deploy the solution

1. In [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], right click the **FTP_EAI_Tutorial** solution, and then select **Build Solution**.

2. Once the build succeeds, right click the **FTP_EAI_Tutorial** solution, and then select **Deploy Solution**.

3. In the deployment window, the **Deployment Endpoint** is a read only entity, and this value is reflected from the **BizTalk Service URL/Namespace** set in the itinerary designer. Enter the Access Control namespace for [!INCLUDE[af_integration](/Token/af_integration_md.md)], Issuer Name, and Shared Secret.

4. Select **Deploy**. The [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] Output pane displays the deployment progress and result. The URL where the bridge is deployed is also displayed in the Output pane.

## See Also
[Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server](/Topic/Tutorial__Using_BizTalk_Bridges_to_Insert_Flat_File_Messages_into_an_On-premises_SQL_Server.md)

