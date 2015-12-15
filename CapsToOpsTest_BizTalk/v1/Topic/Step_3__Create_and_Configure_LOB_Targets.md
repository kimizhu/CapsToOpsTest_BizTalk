---
description: na
keywords: na
pagetitle: Step 3: Create and Configure LOB Targets
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0594fc19-ebfa-4484-b6ef-3e8cdaf1cdc0
---
# Step 3: Create and Configure LOB Targets
Connect to an on-premises LOB application by creating [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s in your [!INCLUDE[af_integration](/Token/af_integration_md.md)] application. [Development and Runtime Architecture: BizTalk Adapter Service](/Topic/Development_and_Runtime_Architecture__BizTalk_Adapter_Service.md) describes how [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s manage connectivity with an on-premises LOB application.

For the scenario used in this tutorial, Northwind stores the sales order data in a **SalesOrder** SQL Server table. The steps in this section demonstrate how to create the **SalesOrder** SQL Server table, how to create an [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to write data into the table, and then finally generate the message schema for inserting data into the table. Specifically:

[Create the SQL Server table](/Topic/Step_3__Create_and_Configure_LOB_Targets.md#BKMK_CreateTable)

[Create the SQL Server LOBTarget](/Topic/Step_3__Create_and_Configure_LOB_Targets.md#BKMK_CreateLOB)

[Generate the schema](/Topic/Step_3__Create_and_Configure_LOB_Targets.md#BKMK_GenSchema)

## <a name="BKMK_CreateTable"></a>Create the SQL Server table
Use these steps to create the **SalesOrder**[!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] table that contains the sales order data. You can create the table in a database called **Orders**.

1. Open [!INCLUDE[ssManStudioFull](/Token/ssManStudioFull_md.md)].

2. Run the following query to create the **SalesOrder** table:

   ```
   CREATE TABLE [dbo].[SalesOrder] (
       [SalesOrderID] int IDENTITY(1,1) NOT NULL,
       [PartNum] int  NOT NULL,
       [DateRequested] datetime  NULL,
       [CompanyCode] varchar(3)  NOT NULL,
       [Qty] int  NOT NULL,
       [UnitAskPrice] float  NULL,
       [ShipDate] datetime  NOT NULL,
       [SellToAddress] varchar(255)  NULL,
       [BillToAddress] varchar(255)  NOT NULL,
       [PartnerContact] varchar(128)  NULL,
       [CustomerComments] varchar(500)  NULL,
       [RFQStatuesId] smallint  NULL
   );
   GO
   ```

3. Confirm the table is created in the target database.

## <a name="BKMK_CreateLOB"></a>Create the SQL Server LOBTarget
Create the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] for the **Insert** operation on the **SalesOrder** table:

1. In the **EAIEDITutorial** project, select the **View** menu, and then select **Server Explorer**.

   > [!NOTE]
   > To create an [!INCLUDE[lobrelay](/Token/lobrelay_md.md)], Visual Studio must be opened with administrator privileges.

2. In **Server Explorer**, right-click **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]s**, and then select **Add BizTalk Adapter Service**. This prompts for the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management URL. Enter the management URL. The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management URL is the path to the ManagementService.svc WCF service hosted in IIS. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) provides more information on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] components within IIS.

   - If the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime is installed locally with the default settings, enter: **http://localhost:8080/BAService/ManagementService.svc/**

   - If the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime is installed remotely with the default settings, enter: **http://ServerName:8080/BAService/ManagementService.svc/**

   Select **OK**.

3. Expand the newly added server, expand **LOB Types**, right-click **SQL**, and select **Add SQL Target**. The **Add a Target** wizard opens.

4. In **Before You Begin**, select **Next**.

5. In **Connection Parameters**, enter the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] details and the credentials to use for the connection. Select **Next**.

   > [!NOTE]
   > You can use the **Advanced** button to build the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] connection URI and also enter the binding properties for the connection.
   > 
   > [The SQL Server Connection URI](http://go.microsoft.com/fwlink/p/?LinkId=228970) provides additional information about how to build the URI. For binding properties, see [Working with BizTalk Adapter for SQL Server Binding Properties](http://go.microsoft.com/fwlink/p/?LinkId=228971).
   > 
   > For this tutorial, leave the default setting as-is for the binding properties.

6. In **Operations**, expand **Tables**, expand **SalesOrder**, select **Insert**, and then select the right arrow. The **Insert** operation is now listed under the **Selected categories** section.

   Select **Next**.

7. In **Runtime Security**, select **Fixed Windows credential**, enter the credentials, and then select **Next**.

   This security type determines how the client message is authenticated with the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. Options include:

   |||
   |-|-|
   |Fixed Username <br /> <br />|Use a username and password created locally on the LOB system. <br /> <br />|
   |Fixed Windows credential <br /> <br />|Use a Windows domain account. <br /> <br />|
   |Custom SOAP Header <br /> <br />|Use a custom-created SOAP header that includes the username and password. <br /> <br />|

8. In **Deployment**, create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] or choose an existing one.

   > [!TIP]
   > A single [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] can be used with multiple [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. There are restrictions based on the security model. As a best practice, group the same security method in one [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. For example, use the same [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to host the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s that use Message Credential or Fixed Windows security type.

   To create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]:

   |||
   |-|-|
   |Namespace <br /> <br />|**Required**. Enter your [!INCLUDE[sb2](/Token/sb2_md.md)] namespace; the LOB relay is created in the [!INCLUDE[sb2](/Token/sb2_md.md)]. The namespace name is available in the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414). <br /> <br />|
   |Issuer Name <br /> <br />|**Required**. The [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name, listed in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkId=517414). <br /> <br />|
   |Issuer Secret <br /> <br />|**Required**. The [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Secret key, listed in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkId=517414). <br /> <br />|
   |Relay Path <br /> <br />|**Required**. Enter the desired name of the relay path. For this tutorial, set this property to **OrderProcessing**. <br /> <br />|
   |Target Sub-path <br /> <br />|**Required**. Enter a sub-path to make this target unique. For example, you can enter **SQLGetOrder**. <br /> <br />|
   |Target runtime URL <br /> <br />|This is automatically populated with the namespace name, relay path, and target sub-path you entered. If using the examples above, it is populated with something like: <br /> <br />`https://MyNamespace.servicebus.windows.net/OrderProcessing/SQLGetOrder` <br /> <br />|
   Select **Next**.

9. In **Summary**, review your values. Select **Create**.

When the wizard completes, select **Finish**. The following events occur in the background:

- The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created in Server Explorer. It can be disabled, started, and deleted. Its configuration can also be exported.

- The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created as an application in IIS. This application uses the Runtime for this specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) describes the IIS components.

#### To use the LOB Target

1. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**, and update the **BizTalk Service URL** property to include your [!INCLUDE[af_integration](/Token/af_integration_md.md)] name. This is the name you entered in [Azure classic portal](http://go.microsoft.com/fwlink/?LinkId=517414) when creating the [!INCLUDE[af_integration](/Token/af_integration_md.md)].

2. Set the security property for the relay endpoint:

   1. Right-click the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] in Server Explorer and select **Properties**.

   2. In the Properties grid, select the ellipsis **(…)** next to the **Runtime Security** property.

   3. In **Edit Security**, select **Fixed Windows Credentials**, and enter username and password to connect to the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)].

   4. Select **OK**.

3. Drag and drop the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] onto the design area. Note the **Entity Name** property of the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. The default value is *Relay-Path_target-sub-path*. If using the examples above, it is *orderprocessing_sqlgetorder*.

4. Open the .config file for the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)], which typically has the *YourRelayPath_target-sub-path.config* naming convention. Enter the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name and issuer secret, as shown:

   ```
   <tokenProvider>
     <sharedSecret issuerName="owner" issuerSecret="issuer_secret" />
   </tokenProvider>
   ```
   Save changes to the config file.

## <a name="BKMK_GenSchema"></a>Generate the schema
Generate the schema for the **Insert** operation on the **SalesOrder** table. You can use the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] you created in the previous step.

1. Right click the **test01/orderprocessing/sqlgetorder** entity in Server Explorer, and then select **Add schemas To EAIEDITutorial**.

   > [!NOTE]
   > This menu property is enabled only if [!INCLUDE[af_integration](/Token/af_integration_md.md)] project is open in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)].

2. In **Schema Generation**, set the file name prefix to **EAIEDITutorial_SalesOrder_**, and leave the folder name to its default value of **LOB Schemas**.

   Select credential Type as **Windows** and then select **OK**.

   An **LOB Schemas** folder is created within the project and the generated schemas are added under it. The schema for the Insert operation on the **SalesOrder** table is created with the *EAIEDITutorial_SalesOrder_TableOperation.dbo.SalesOrder.xsd* name.

## See Also
[Create and Deploy the BizTalk Services Project](/Topic/Create_and_Deploy_the_BizTalk_Services_Project.md)

