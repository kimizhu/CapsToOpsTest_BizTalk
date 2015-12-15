---
description: na
keywords: na
pagetitle: Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8a58fb7-55dd-4c4a-a683-8688d7bda69c
---
# Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database
This tutorial provides guidance on how to use the **Enrich** stage within a [!INCLUDE[af_integration](/Token/af_integration_md.md)] bridge to look up data from a [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)]. To demonstrate how the bridge looks up data from [!INCLUDE[ssSDS](/Token/ssSDS_md.md)], consider a scenario in which a flat-file message is picked from an FTP server, is processed using a [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)], and the data from the flat file is finally inserted into an on-premises SQL Server. In addition to demonstrating how to look up data from [!INCLUDE[ssSDS](/Token/ssSDS_md.md)], this tutorial also provides guidance on the following features::

- Processing flat file messages by using [!INCLUDE[one-way](/Token/one-way_md.md)]. For more information, see [Flat-file Support In One-Way Bridge](http://go.microsoft.com/fwlink/p/?LinkID=248909).

- Creating a flat-file schema by using the Flat File Schema wizard. For more information, see [How to Use the Flat File Schema Wizard](http://go.microsoft.com/fwlink/p/?LinkId=248911).

- Using an FTP source to send messages to an [!INCLUDE[one-way](/Token/one-way_md.md)]. For more information, see [Using FTP Source](http://go.microsoft.com/fwlink/p/?LinkId=248912).

- Tracking a message as it gets processed through the bridges. For more information, see [Operational Tracking of Messages Processed by the Bridge](http://go.microsoft.com/fwlink/p/?LinkId=250919)

With the support for processing flat-file messages, you can use a one-way bridge to process XML as well as flat-file messages, using the same bridge endpoint. However, you would still need to create and add the schema of the flat file message to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. The **Flat File Schema** wizard does that for you. If you already have a flat-file message, you can use the wizard to generate the schema for that flat-file message and also add it to the project. You can then put a flat file message on an FTP location and the bridge could consume the flat-file message through an FTP source, process it, and then send to the required destination endpoint. And finally, you could track the message as it gets processed within each stage of the bridge. Organizations can tie all these features together into an end-to-end scenario that to meet their business requirements. Using the following business scenario, this tutorial demonstrates these features and some other features in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

## Business Scenario
Northwind Traders is a healthcare service provider that handles medical insurance claims for an insurance provider, Humongous Insurance. Northwind sends insurance claims as flat-file messages to Humongous Insurance. Humongous Insurance processes these claims and stores them in-house using an on-premises SQL Server database. Humongous Insurance wants to deploy this business process as an application on [!INCLUDE[azure_1](/Token/azure_1_md.md)]. Humongous Insurance decides to use the integration capabilities provided with [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] to deploy this application on the cloud.

Here are the series of steps that Humongous Insurance and Northwind Traders have to perform at their ends to develop, configure, and deploy the application.

Humongous Insurance creates an [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] using [!INCLUDE[af_integration](/Token/af_integration_md.md)]. Within this project, it does the following:

Uses a sample flat-file instance message that it receives from Northwind Traders (out of band, over e-mail), to create the flat-file message schema. Humongous Insurance needs this schema to validate and process flat-file messages that it receives from Northwind.

Adds an FTP source component to the project. The FTP source represents the FTP server where Northwind Traders drops the flat-file message.

Adds a one-way bridge to process the flat-file messages that it receives from Northwind Traders. Within the bridge, Humongous Insurance does the following:

- Uses a transform to convert the message received from Northwind to a format that is required to insert the message into a SQL Server database table where Humongous Insurance maintains all the insurance claims.

- Performs *data enrichment* on the incoming message. Through data enrichment, Humongous Insurance enriches the message to include information which was not part of the original message that Northwind Traders sent. For example, in this scenario, the flat-file message from Northwind Traders only includes a *claim type* information. But Humongous Insurance must include the *claim type description* as well in message that is inserted into the on-premise SQL Server database. So, to achieve this data enrichment, Humongous Insurance looks up a [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table (which it maintains to map claim type to claim description) to see which claim type description maps to the claim type in the incoming message and then updates the message that is finally inserted in the on-premises SQL Server database to include the claim type description.

- *Promotes* certain elements in the message as properties that it can use to track the message as the [!INCLUDE[bridge](/Token/bridge_md.md)] processes it.

Finally, Humongous adds a [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] that represents the on-premises SQL Server where the data from the message has to be inserted.

Humongous Insurance builds and deploys this solution on [!INCLUDE[sb2](/Token/sb2_md.md)].

Once the solution is deployed, Northwind Traders drops a flat-file message for an insurance claim at the specified location on the FTP Server. The [!INCLUDE[one-way](/Token/one-way_md.md)] consumes the message and inserts into the SQL Server database. The following illustration represents the same scenario.

![](/Image/FFBridge-Scenario.gif)

## How to Use This Article
This tutorial is written around a sample, **FlatFile_Bridge.zip**, which is available as part of the download from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/p/?LinkID=249449). You could either use the sample and go through this tutorial to understand how the sample was built or use this tutorial to create your own application. This tutorial is targeted towards the second approach so that you understand how this application was built. Also, as far as possible, the tutorial is consistent with the sample and uses the same names for artifacts (for example, schemas, transforms, and so on) as used in the sample.

Even though Microsoft recommends that you follow the tutorial to understand the concepts and procedures, if you wish to use the sample, do the following:

- Download the **FlatFile_Bridge.zip** package, extract the **FlatFile_Bridge** sample, and make relevant changes like providing your service namespace, issuer name, issuer key, updating the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)], and FTP components to include your specific server details, and so on. After making required changes, build and deploy the application.

- Drop a test message at the FTP location configured as part of the solution and verify that the application works as expected. If the message is successfully processed, it is routed to the SQL Server and you can verify that new records are entered in the Claims table.

## In This Section

- [Step 1: Set Up Your Computer](/Topic/Step_1__Set_Up_Your_Computer.md)

- [Step 2: Create the Enterprise Application Integration Project](/Topic/Step_2__Create_the_Enterprise_Application_Integration_Project.md)

- [Step 3: Generate the Schema for the Flat File Message](/Topic/Step_3__Generate_the_Schema_for_the_Flat_File_Message.md)

- [Step 4: Add an FTP Source](/Topic/Step_4__Add_an_FTP_Source.md)

- [Step 5: Create and Configure the LOB Target](/Topic/Step_5__Create_and_Configure_the_LOB_Target.md)

- [Step 6: Configure a One-Way Bridge](/Topic/Step_6__Configure_a_One-Way_Bridge.md)

- [Step 7: Transform the Flat File Schema to the Insert Schema](/Topic/Step_7__Transform_the_Flat_File_Schema_to_the_Insert_Schema.md)

- [Step 8: Connect the Components on the Bridge Configuration Surface](/Topic/Step_8__Connect_the_Components_on_the_Bridge_Configuration_Surface.md)

- [Step 9: Build and Deploy the Solution](/Topic/Step_9__Build_and_Deploy_the_Solution.md)

- [Step 10: Test the Solution](/Topic/Step_10__Test_the_Solution.md)

## See Also
[Developing Enterprise Applications with Azure](http://msdn.microsoft.com/en-us/library/7a2eb23f-da18-438f-8d25-9852aa70fae1)

