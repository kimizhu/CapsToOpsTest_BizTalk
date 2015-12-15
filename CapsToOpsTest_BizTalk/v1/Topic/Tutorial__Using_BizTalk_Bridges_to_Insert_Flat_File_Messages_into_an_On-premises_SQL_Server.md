---
description: na
keywords: na
pagetitle: Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 346839fa-735d-4760-835b-f4a04f25a228
---
# Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server
This tutorial provides instructions on how to configure a [!INCLUDE[af_integration](/Token/af_integration_md.md)] solution that receives a flat-file message from an FTP server, processes it through a [!INCLUDE[bridge](/Token/bridge_md.md)] deployed under the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription on [!INCLUDE[azure_1](/Token/azure_1_md.md)], and then inserts the message into an on-premises [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] database.

## Business Scenario
Fabrikam and Contoso are two business partners. Fabrikam (the retailer) sends sales order messages to Contoso (the supplier). Contoso maintains all the sales order data in table called Orders, which is housed in a [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] database within Contoso’s premises. Fabrikam sends flat-file messages to Contoso using an FTP server. Hence, Contoso has to implement a solution that enables the following:

- Contoso must pull the flat file messages from the FTP server at which Fabrikam drops the sales order messages.

- Contoso must process the message received from Fabrikam and map it to the message for inserting the sales order in its [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] database.

To enable this scenario, Contoso does the following:

- Generates the schema of the flat-file message that it will receive from Fabrikam.

- Configures an [!INCLUDE[one-way](/Token/one-way_md.md)] as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] to enable message validation and transformation. This [!INCLUDE[bridge](/Token/bridge_md.md)] takes a flat-file message, validates it against the schema generated earlier, and then transforms it to the schema required to enter a message into the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] database.

- Uses [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] to connect to the on-premise [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] database from the [!INCLUDE[one-way](/Token/one-way_md.md)] deployed under the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

## Before You Begin this Tutorial
For instructions on how to prepare for the [!INCLUDE[af_integration](/Token/af_integration_md.md)] scenario, see [Create the project in Visual Studio](/Topic/Create_the_project_in_Visual_Studio.md).

## Sample Based on this Tutorial
You can also look at the sample that is based on this tutorial. A sample (**FTP_EAI_Tutorial**) is available from the list of samples available at [http://go.microsoft.com/fwlink/?LinkId=247973](http://go.microsoft.com/fwlink/?LinkId=247973).

## In This Section

- [Step 1: Create the BizTalk Services Project Now](/Topic/Step_1__Create_the_BizTalk_Services_Project_Now.md)

- [Step 2: Generate the Schema for the Flat-file Message](/Topic/Step_2__Generate_the_Schema_for_the_Flat-file_Message.md)

- [Step 3: Add an FTP Source](/Topic/Step_3__Add_an_FTP_Source.md)

- [Step 4: Create and Configure the LOB Target](/Topic/Step_4__Create_and_Configure_the_LOB_Target.md)

- [Step 5: Transform the Flat File Schema to the Insert Schema for OrderDetails Table](/Topic/Step_5__Transform_the_Flat_File_Schema_to_the_Insert_Schema_for_OrderDetails_Table.md)

- [Step 6: Configure an XML One-Way Bridge](/Topic/Step_6__Configure_an_XML_One-Way_Bridge.md)

- [Step 7: Build and Deploy the Project](/Topic/Step_7__Build_and_Deploy_the_Project.md)

- [Step 8: Test the Solution](/Topic/Step_8__Test_the_Solution.md)

## See Also
[Tutorials and Samples](/Topic/Tutorials_and_Samples.md)

