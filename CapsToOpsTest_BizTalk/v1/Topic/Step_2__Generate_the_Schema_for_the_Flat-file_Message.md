---
description: na
keywords: na
pagetitle: Step 2: Generate the Schema for the Flat-file Message
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1bfcd81a-c3ff-4c88-b93b-0b1032f38122
---
# Step 2: Generate the Schema for the Flat-file Message
As described in the business scenario, Fabrikam sends a flat file message to Contoso. For Contoso, to process the message using the [!INCLUDE[bridge](/Token/bridge_md.md)], it must have the schema of the flat-file message added to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] solution. [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK provides a **Flat File Schema Wizard** that generates a flat-file schema using an existing flat-file instance message. Contoso uses the flat-file message instance message that it received from Fabrikam (out of band, over e-mail or through another medium) and then uses the **Flat File Schema Wizard** to create the schema. To use the wizard, see [How to Use the Flat File Schema Wizard](/Topic/How_to_Use_the_Flat_File_Schema_Wizard.md).

For this tutorial, let us assume that a flat-file message (**ORDERS.txt**) is sent to Contoso. Contoso uses the **Flat File Schema Wizard** and generates the **PO.xsd** flat-file message schema. Both the instance message and the message schema are in the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=247973) sample. Add the PO.xsd schema to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] project you created earlier.

## See Also
[Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server](/Topic/Tutorial__Using_BizTalk_Bridges_to_Insert_Flat_File_Messages_into_an_On-premises_SQL_Server.md)

