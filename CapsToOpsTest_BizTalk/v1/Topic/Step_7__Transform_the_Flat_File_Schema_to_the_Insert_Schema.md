---
description: na
keywords: na
pagetitle: Step 7: Transform the Flat File Schema to the Insert Schema
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1e209ac-0c75-42ea-93bc-61a83eba849b
---
# Step 7: Transform the Flat File Schema to the Insert Schema
This section demonstrates how to map the elements in the incoming flat file message to the elements in the **Insert** message for the **Claims** table. To understand which elements in the source schema map to which elements in the destination schema, it is important to first look at the two schemas.

![](/Image/FFBridge-TwoSchemas.gif)

The following table lists the mapping requirements and the map operations to use to accomplish the message transformation:

|What to map? <br /> <br />|How to achieve? <br /> <br />|
|----------------|-------------------|
|All the elements in the flat-file schema map to relevant elements in the Insert message schema. For example, **ClaimID** maps to **ClaimID**, **ClaimType** maps to **ClaimType**, and so on. <br /> <br />|You directly connect the two nodes in the two schemas. <br /> <br />|
|Because the **ClaimTypeDescription** element in the Insert message schema gets its value by using the lookup configuration defined earlier, **ClaimType** element in the flat file schema also maps to the **ClaimTypeDescription** element in the Insert schema by using a **Data Lookup** map operation. <br /> <br />|See [To use a Data Lookup map operation](/Topic/Step_7__Transform_the_Flat_File_Schema_to_the_Insert_Schema.md#BKMK_DataLookup) <br /> <br />|
After defining the map, include it in the bridge configuration defined in [Step 6: Configure a One-Way Bridge](/Topic/Step_6__Configure_a_One-Way_Bridge.md).

### To use a Data Lookup map operation

1. Right-click the FlatFile_Bridge project, point to **Add**, and then click **New Item**.

2. In the **Add New Item** dialog box, select **Map**, specify the map name as **FF_SQL_Transform.trfm**, and then click **OK**.

3. On the map surface, select the source schema to **InsuranceClaim.xsd** and the destination schema to **FlatFile_Bridge_TableOperation.dbo.Claims.xsd** (Insert operation).

4. On the **Toolbox**, from the **Misc Operations** category, drag-and-drop a **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] on the map surface. Double-click the map operation, and for the **Property Name** text box, enter **ClaimTypeDescription**, and then click **OK**.

5. Connect the **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] to the **ClaimTypeDescription** element in the destination schema.

   As part of the bridge configuration, you had already configured the lookup such that the claim type description is already retrieved from the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] and is assigned to a **ClaimTypeDescription** property that gets created at runtime. Using the **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)], you assign the value of that property to the **ClaimTypeDescription** element in the destination schema.

   Map the other elements in the source and destination schemas, as shown below.

   ![](/Image/FFBridge-ConfigMap.gif)

   Save the map.

6. Save the project.

### To add the map to the bridge configuration

1. In the **FlatFile_Bridge** project, open the .bridgeconfig file, and select the **Xml Transform** activity.

2. From the **Properties** pane, click the ellipsis button **(…)** against the **Maps** property to open the **Map Selection** dialog box.

3. Select the check box for the **FF_SQL_Transform** map and then click **OK**.

4. Save changes to the project.

## See Also
[Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md)

