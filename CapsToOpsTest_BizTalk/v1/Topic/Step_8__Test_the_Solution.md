---
description: na
keywords: na
pagetitle: Step 8: Test the Solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b11e5129-5eb0-4f50-b2d9-33bd48f13746
---
# Step 8: Test the Solution
In this step, we test the solution by dropping a flat-file message to a folder on the FTP Server. The [!INCLUDE[one-way](/Token/one-way_md.md)] should consume this message, process it, and then insert the values into the **OrderDetails** table in the **Orders** database [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)].

### To send a message to the bridge

1. Locate the **Orders.txt** message from the location you downloaded the **FTP_EAI_Tutorial** sample and copy it to a folder on the FTP Server. The [!INCLUDE[bridge](/Token/bridge_md.md)] you configured as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] must be configured to pick messages from this folder. The Orders.txt message has the following content:

   ```
   Ord123|Item201;20;50|Item202;100;20
   ```

2. Wait for the message to disappear. Now go to the **OrderDetails** table in the **Orders** database and verify the new values are inserted:

   ![](/Image/FTP_EAI_Tutorial_DbOutput.jpg)

   Note that the values correspond to the data in the flat-file message that you dropped to the FTP server.

3. Because you configured the [!INCLUDE[bridge](/Token/bridge_md.md)] to track message properties, you can also view the tracked data. Go to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] registered for your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription, select the **Tracking** tab, select the **Route: Route** activity information, and then from the command bar, select **Details**. In the pop-up window, notice that the **OrderId** and **TotalAmount** properties are tracked and their values are also displayed:

   ![](/Image/FTPEAITutorial_TrackProps.jpg)

   Note that the tracked values correspond to the values that are inserted into the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] database.

## See Also
[Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server](/Topic/Tutorial__Using_BizTalk_Bridges_to_Insert_Flat_File_Messages_into_an_On-premises_SQL_Server.md)

