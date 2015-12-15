---
description: na
keywords: na
pagetitle: Step 10: Test the Solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46863ce2-1012-4e59-aeca-b3d4e9212150
---
# Step 10: Test the Solution
This section demonstrates how to test the solution by dropping a flat-file message to a folder on the FTP Server. The one-way bridge consumes this message, processes it, and then writes the values into the **Claims** table in the **InsuranceData** database in the on-premises SQL Server instance for Humongous Insurance.

### To send a message to the bridge

1. Locate the **SampleInsuranceClaim.txt** message under the location where you downloaded the **FlatFile_Bridge** sample. See the contents of the message, which resemble the following:

   ```
   101|HI|1000.0|John;RedmondWay;Seattle;Washington|1234567
   ```
   Notice the second element, **HI**. This is type of claim that is being processed. Also, notice that there is no claim description for this claim type in the message that is sent by Northwind.

   Copy the message to the **ReceiveFFMessage** folder on the FTP Server. The bridge you configured as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] picks messages from this folder.

2. Wait for the message to disappear. Now go to the **Claims** table in the **InsuranceData** database and verify if the new values have been inserted.

   Notice that even though the input flat-file message did not have a claim description, the **Claims** table has the value “HealthInsurance” inserted for the **ClaimTypeDescription** column. This value was included in the message by using the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] lookup configured as part of the bridge and the transform. If you want to see how the lookup configuration looks up value from the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table, change the value in the **ClaimTypeDescription** in the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table and then drop another message to the FTP location. The next message that is inserted in the **Claims** table must have the new value you entered in the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)].

   ![](/Image/FFBridge_SQLTable.gif)

3. Because you configured the bridge to track message properties, you can also view the tracked data from the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. Log in to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], and from the left pane, click **Tracking**. In the right pane, under the **Messages** tab, see the different levels of tracking info. Select a row, and from the bottom of the screen click **Details** to see more details about that event. For example, the following screenshot shows the detailed info about the Route activity.

   ![](/Image/FFBridge_ViewTrackData.gif)

   Note that it shows the values for **ClaimType** and **ClaimTypeDescription** properties. That’s because you selected these properties to be tracked (see [Configure Tracking](/Topic/Step_6__Configure_a_One-Way_Bridge.md#BKMK_Tracking)) when you configured tracking as part of the bridge configuration.

   For more information about how to track messages, see [Tracking Messages in BizTalk Services portal](/Topic/Tracking_Messages_in_BizTalk_Services_portal.md).

## See Also
[Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md)

