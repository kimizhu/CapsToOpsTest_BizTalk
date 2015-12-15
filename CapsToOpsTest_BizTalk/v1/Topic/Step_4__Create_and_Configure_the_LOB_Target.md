---
description: na
keywords: na
pagetitle: Step 4: Create and Configure the LOB Target
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5b8de56-9c4e-4f89-b4e5-8996850f6226
---
# Step 4: Create and Configure the LOB Target
Create [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s in your [!INCLUDE[af_integration](/Token/af_integration_md.md)] application to connect to an on-premises LOB application. [Development and Runtime Architecture: BizTalk Adapter Service](/Topic/Development_and_Runtime_Architecture__BizTalk_Adapter_Service.md) describes how [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s manage connectivity with an on-premises LOB application.

This section lists how to create a [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] table where the sales order data is inserted, how to create a [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] and target for the **Insert** operation on the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] table, and how to generate the schema for the **Insert** operation on the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] table. Specifically:

[Create the SQL Server table](/Topic/Step_4__Create_and_Configure_the_LOB_Target.md#BKMK_CreateTable)

[Create a SQL Server LOBTarget](/Topic/Step_4__Create_and_Configure_the_LOB_Target.md#BKMK_CreateLOB)

[Generate the Schema](/Topic/Step_4__Create_and_Configure_the_LOB_Target.md#BKMK_GenSchema)

## <a name="BKMK_CreateTable"></a>Create the SQL Server table
Use these steps to create the **OrderDetails** table in [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] in which the sales order data is inserted. The script is also available in the **FTP_EAI_Tutorial** sample at [http://go.microsoft.com/fwlink/?LinkId=247973](http://go.microsoft.com/fwlink/p/?LinkId=247973). This script assumes that you already have an **Orders** database created.

1. Open [!INCLUDE[ssManStudioFull](/Token/ssManStudioFull_md.md)].

2. Run the following script to create the **OrderDetails** table:

   ```
   USE [Orders]
   GO
   /****** Object:  Table [dbo].[OrderDetails]    Script Date: 04/02/2012 20:35:57 ******/
   IF  EXISTS (SELECT * FROM sys.objects WHERE object_id = OBJECT_ID(N'[dbo].[OrderDetails]') AND type in (N'U'))
   DROP TABLE [dbo].[OrderDetails]
   GO
   USE [Orders]
   GO
   /****** Object:  Table [dbo].[OrderDetails]    Script Date: 04/02/2012 20:35:57 ******/
   SET ANSI_NULLS ON
   GO
   SET QUOTED_IDENTIFIER ON
   GO
   SET ANSI_PADDING ON
   GO
   CREATE TABLE [dbo].[OrderDetails](
   [Id] [int] IDENTITY(1,1) NOT NULL,
   [OrderId] [varchar] (200),
   [QuantityOrdered] [int],
   [TotalAmount] [int]
   PRIMARY KEY CLUSTERED 
   (
   [Id] ASC
   )WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON) ON [PRIMARY]
   ) ON [PRIMARY]
   GO
   SET ANSI_PADDING OFF
   GO
   ```

3. Confirm the table is created in the database.

## <a name="BKMK_CreateLOB"></a>Create a SQL Server LOBTarget
Create the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] and the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] for the **Insert** operation on the **OrderDetails** table:

1. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], from **Server Explorer**, right-click **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]s**, and then select **Add BizTalk Adapter Service**. This prompts for the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management URL. Enter the management URL. The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management URL is path to the ManagementService.svc WCF service hosted in IIS. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) provides more information on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] components within IIS.

   - If the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime is installed locally with the default settings, enter: **http://localhost:8080/BAService/ManagementService.svc/**

   - If the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime is installed remotely with the default settings, enter: **http://ServerName:8080/BAService/ManagementService.svc/**

   Select **OK**.

2. Expand the newly added server, expand **LOB Types**, right-click **SQL**, and select **Add SQL Target**. The **Add a Target** wizard opens.

3. In **Before You Begin**, select **Next**.

4. On **Connection Parameters**, enter the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] details and the credentials to use for the connection. Select **Next**.

   > [!NOTE]
   > You can use the **Advanced** button to build the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] connection URI and also enter the binding properties for the connection.
   > 
   > [The SQL Server Connection URI](http://go.microsoft.com/fwlink/p/?LinkId=228970) provides additional information about how to build the URI. For binding properties, see [Working with BizTalk Adapter for SQL Server Binding Properties](http://go.microsoft.com/fwlink/p/?LinkId=228971).
   > 
   > For this tutorial, leave the default setting as-is for the binding properties.

5. In **Operations**, expand **Tables**, expand **OrderDetails**, select **Insert**, and then select the right arrow. The **Insert** operation is now listed under the **Selected operations** section.

   Select **Next**.

6. In **Runtime Security**, select **Fixed Windows credential**, enter the credentials, and then select **Next**.

   This security type determines how the client message is authenticated with the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. Options include:

   |||
   |-|-|
   |Fixed Username <br /> <br />|Using a username and password created locally on the LOB system. <br /> <br />|
   |Fixed Windows credential <br /> <br />|Use a Windows domain account. <br /> <br />|
   |Custom SOAP Header <br /> <br />|You create a custom SOAP header to include the username and password. <br /> <br />|
   |Message Credential <br /> <br />|You are including the logon credentials in the WS-Security header of the message. <br /> <br />|

7. In **Deployment**, choose an existing [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] or create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)].

   > [!TIP]
   > A single [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] can be used with multiple [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. There are restrictions based on the security model. As a best practice, group the same security method in one [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. For example, use the same [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to host the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s that use Message Credential or Fixed Windows security type.

   To create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]:

   |||
   |-|-|
   |Namespace <br /> <br />|**Required**. Enter your [!INCLUDE[sb2](/Token/sb2_md.md)] namespace; the LOB relay is created in the [!INCLUDE[sb2](/Token/sb2_md.md)]. The namespace name is listed in the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414). <br /> <br />For example, if *myNamespace* is the namespace, this updates the Management address to:`http://MyServer:8080/BAService/ManagementService.svc/myNamepsace` <br /> <br />|
   |Issuer Name <br /> <br />|**Required**. Enter a valid [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name. <br /> <br />|
   |Issuer Secret <br /> <br />|**Required**. Enter a valid[!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Secret key. <br /> <br />|
   |Relay Path <br /> <br />|**Required**. Enter the desired name of the relay path. For this tutorial, set this property to **SQLLOBRelay**. <br /> <br />|
   |Target Sub-path <br /> <br />|**Required**. Enter a sub-path to make this target unique. For example, you can enter **OrderDetails**. <br /> <br />|
   |Target runtime URL <br /> <br />|This is automatically populated with the namespace name, relay path, and target sub-path you entered. If using these examples, it is populated with something like: <br /> <br />`https://MyNamespace.servicebus.windows.net/SQLLOBRelay/OrderDetails` <br /> <br />|
   Select **Next**.

8. In **Summary**, review your values. Select **Create**.

When the wizard completes, select **Finish**. The following activities occur in the background:

- The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created in Server Explorer. It can be disabled, started, and deleted. Its configuration can also be exported.

- The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created as an application in IIS. This application uses the Runtime for this specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) describes the IIS components.

**To use the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]:**

1. Set the **Runtime Security** property for the relay endpoint:

   1. Right-click the relay endpoint in Server Explorer and select **Properties**.

   2. In **Properties**, select the ellipsis **(…)** next to the **Runtime Security** property.

   3. In **Edit Security**, select **Fixed Windows Credentials**, and enter username and password to connect to the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)].

   4. Select **OK**.

2. Drag and drop the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] onto the design area. Note the **Entity Name** property of the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. The default value is *Relay-Path_target-sub-path*. If using the examples above, it is *sqllobrelay_orderdetails*.

3. Open the .config file for the LOB target, which typically has the *YourRelayPath_target-sub-path.config* naming convention. Enter the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name and issuer secret, as shown:

   ```
   <tokenProvider>
     <sharedSecret issuerName="owner" issuerSecret="issuer_secret" />
   </tokenProvider>
   ```
   Save changes to the config file.

## <a name="BKMK_GenSchema"></a>Generate the Schema
Generate the schema for the **Insert** operation on the **OrderDetails** table:

1. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], in the **Server Explorer**, right click the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] you just created, and then select **Add schemas to FTP_EAI_Tutorial**. The **Schema Generation** dialog opens.

2. Set the file name prefix to **FTP_EAI_Tutorial_**. Leave the folder name to its default value of **LOB Schemas**.

3. Select credential type as **Windows** to use Windows authentication to connect to [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)], and then select **OK**.

   The schemas are added to the **FTP_EAI_Tutorial** project under the **LOB Schemas** folder.

## See Also
[Tutorial: Using BizTalk Bridges to Insert Flat File Messages into an On-premises SQL Server](/Topic/Tutorial__Using_BizTalk_Bridges_to_Insert_Flat_File_Messages_into_an_On-premises_SQL_Server.md)

