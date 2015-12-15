---
description: na
keywords: na
pagetitle: Step 9: Build and Deploy the Solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a4f9225-bd58-4530-98d8-5eb0200c58ee
---
# Step 9: Build and Deploy the Solution
By now, you have finished creating the application. In this step, you build and deploy the application under your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

### To build and deploy the solution

1. In Visual Studio, right click the **FlatFile_Bridge** solution, and then click **Build Solution**.

2. Once the build succeeds, right click the **FlatFile_Bridge** solution, and then click **Deploy Solution**.

3. In the deployment window, the **Deployment Endpoint** is a read-only property and the value is derived from the **BizTalk Service URL/Namespace** set in the message flow surface. However, you must provide the ACS Namespace for [!INCLUDE[af_integration](/Token/af_integration_md.md)], Issuer Name, and Shared Secret.

4. Click **Deploy**. The Visual Studio Output pane displays the deployment progress and result. The URL where the bridge is deployed is also displayed in the Output pane. For this tutorial, the bridge is deployed at `http://*<mybiztalkservicename>*.biztalk.windows.net/default/**ClaimsProcessing**`.

## See Also
[Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md)

