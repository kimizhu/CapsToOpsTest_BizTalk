---
description: na
keywords: na
pagetitle: Step 6: Build and Deploy the Project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed997cf1-37f1-4810-b0ce-6ad174ee7bf7
---
# Step 6: Build and Deploy the Project
Steps to build and deploy the [!INCLUDE[af_integration](/Token/af_integration_md.md)] solution.

### To build and deploy the solution

1. In [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], right click the **EAIEDITutorial** solution, and then select **Build Solution**.

2. Once the build succeeds, right click the **EAIEDITutorial** solution, and then select **Deploy Solution**.

3. In the deployment window, the **Deployment Endpoint** is a read-only entity and the value is derived from the **BizTalk Service URL/Namespace** set in the message flow area. However, you must provide the Access Control Namespace for [!INCLUDE[af_integration](/Token/af_integration_md.md)] and its Issuer Name and Shared Secret.

4. Select **Deploy**. The [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] Output pane displays the deployment progress and result. The URL where the [!INCLUDE[bridge](/Token/bridge_md.md)] is deployed is also displayed in the Output pane.

## See Also
[Create and Deploy the BizTalk Services Project](/Topic/Create_and_Deploy_the_BizTalk_Services_Project.md)

