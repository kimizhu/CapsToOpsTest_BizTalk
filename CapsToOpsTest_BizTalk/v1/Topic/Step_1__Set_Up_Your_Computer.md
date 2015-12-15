---
description: na
keywords: na
pagetitle: Step 1: Set Up Your Computer
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca51fe22-936a-4b48-a449-75eadadb684d
---
# Step 1: Set Up Your Computer
This topic provides you with the information and pointers to set up your computer on which you will perform the steps to set up the hybrid integration scenario described in [Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md). You must do the following to set up your computer:

- Install **[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK**. You can download the installer from [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057). You use this SDK to configure and deploy the [!INCLUDE[one-way](/Token/one-way_md.md)] that picks flat-file messages from FTP Server, processes it, routes it to a relay endpoint, which then inserts the records into a SQL Server database.

- Install **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**. You use this to expose the **Insert** operation on a SQL Server database table as a relay endpoint on [!INCLUDE[sb2](/Token/sb2_md.md)]. You can download the installer from [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057). Refer to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] installation guide at [http://go.microsoft.com/fwlink/?LinkId=237092](http://go.microsoft.com/fwlink/?LinkId=237092) to install the software prerequisites for [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK and [!INCLUDE[lobconnect](/Token/lobconnect_md.md)].

   > [!NOTE]
   > Typically, if you were connecting to any other line-of-business (LOB) application by using [!INCLUDE[lobconnect](/Token/lobconnect_md.md)], you would also install client libraries for that specific LOB application. However, in this case, because the connection is to a SQL Server instance, explicitly installing client libraries is not required because they are already installed as part of .NET Framework.

- Install the **WCF LOB Adapter SDK**. This is required for installing the Adapter Pack on the computer.

- Install the **Adapter Pack**. This contains the SQL adapter that is required to establish connectivity to a SQL Server database and for exposing operations on SQL Server database tables.

## See Also
[Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md)

