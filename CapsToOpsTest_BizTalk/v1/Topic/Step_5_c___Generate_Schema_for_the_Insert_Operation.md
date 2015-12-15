---
description: na
keywords: na
pagetitle: Step 5(c): Generate Schema for the Insert Operation
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70c286a6-3be0-4de4-b70c-011cbaf26917
---
# Step 5(c): Generate Schema for the Insert Operation
So far, we have the schema for the flat-file message, the FTP source that represents the FTP Server, and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] for connectivity to the on-premise SQL Server. But we still require the schema of the message required to perform an **Insert** operation on the **Claims** table in the on-premise SQL Server database. This step demonstrates how to generate that schema.

### To generate the schema for Insert operation

1. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], in the **Server Explorer**, right click the LOB target you created, and then click **AddSchemasToFlatFile_Bridge**. The **Schema Generation** dialog pops up.

2. Set the file name prefix to **FlatFile_Bridge_**. Leave the folder name to its default value of **LOB Schemas**.

3. Select credential Type as **Windows** to use Windows authentication to connect to SQL Server, and then click **OK**.

   ![](/Image/FFBridge-GenerateSchema.gif)

   The schemas are added to the **FlatFile_Bridge** project under the **LOB Schemas** folder. The schema that corresponds to the **Insert** operation on the **Claims** table has the name **FlatFile_Bridge_TableOperation.dbo.Claims.xsd**. The structure of the schema resembles the following:

   ![](/Image/FFBridge-ClaimsSchema.gif)

4. Save changes to the project.

## See Also
[Step 5: Create and Configure the LOB Target](/Topic/Step_5__Create_and_Configure_the_LOB_Target.md)

