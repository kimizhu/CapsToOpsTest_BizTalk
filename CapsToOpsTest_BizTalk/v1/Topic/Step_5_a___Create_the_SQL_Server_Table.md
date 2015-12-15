---
description: na
keywords: na
pagetitle: Step 5(a): Create the SQL Server Table
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b146b641-8e64-4f4d-aa72-f774ed1e1a9e
---
# Step 5(a): Create the SQL Server Table
In this step, you create the SQL Server table in which the insurance claims received from Northwind Traders are inserted. The name of the table is **Claims**. You can either copy-paste the script provided in this topic or use the script (*OnPremSQLServer_Claims.sql*) included as part of the **FlatFile_Bridge** solution available from [http://go.microsoft.com/fwlink/?LinkID=249449](http://go.microsoft.com/fwlink/?LinkID=249449). The script assumes that you already have an **InsuranceData** database created and creates the **Claims** table under that database.

### To create the SQL Server table

1. Open SQL Server Management Studio and run the following query against the database where you want to create the **Claims** table.

   ```
   USE [InsuranceData]
   GO

   /****** Object:  Table [dbo].[Claims]    Script Date: 04/21/2012 15:24:01 ******/
   SET ANSI_NULLS ON
   GO

   SET QUOTED_IDENTIFIER ON
   GO

   SET ANSI_PADDING ON
   GO

   CREATE TABLE [dbo].[Claims](
   [ID] [int] IDENTITY(1,1) NOT NULL,
   [ClaimID] [int] NULL,
   [ClaimType] [varchar](10) NULL,
   [ClaimTypeDescription] [varchar](50) NULL,
   [ClaimAmount] [float] NULL,
   [Name] [varchar](30) NULL,
   [Address] [varchar](100) NULL,
   [City] [varchar](30) NULL,
   [State] [varchar](30) NULL,
   [PolicyId] [varchar](30) NULL,
   [CoveragePeriod] [datetime] NULL,
   PRIMARY KEY CLUSTERED 
   (
   [ID] ASC
   )WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON) ON [PRIMARY]
   ) ON [PRIMARY]

   GO

   SET ANSI_PADDING OFF
   GO
   ```

2. Verify that the table is created in the target database.

## See Also
[Step 5: Create and Configure the LOB Target](/Topic/Step_5__Create_and_Configure_the_LOB_Target.md)

