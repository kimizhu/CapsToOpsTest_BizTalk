---
description: na
keywords: na
pagetitle: Create a SQL Server LOB target to insert purchase order
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8cad1f7-3bca-48b6-9ded-d02a1322cdc8
---
# Create a SQL Server LOB target to insert purchase order
This topic provides instructions on how to create an SQL Server [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] within the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. You use this [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to insert customer order data into the **Orders** table in the **CloudCarDatabase**. You must have already created the database and the table by using the **CreateDatabaseSchema_CloudCar.sql** script provided with the sample available in the MSDN code gallery at [http://go.microsoft.com/fwlink/p/?LinkId=324220](http://go.microsoft.com/fwlink/p/?LinkId=324220).

### To create an SQL Server LOB target

1. Add a [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] server. This is the server where you installed the Runtime component of [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]. To add a [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] server, from the Server Explorer in Visual Studio, right-click **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**s, and select **Add [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**. In the **Add [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** dialog box, enter the URL of the WCF service that monitors that [!INCLUDE[sb2](/Token/sb2_md.md)] relay service, and then select **OK**.

   ![](/Image/AFINT_PG_AddSBServer.gif)

   Because you have all the components of [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] installed on the same computer, the URL for that service will be `http://localhost:8080/BAService/ManagementService.svc/`.

   > [!NOTE]
   > If you installed [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime component on a separate computer, you must replace ‘localhost’ in the above URL with the name of that computer.

2. Expand the newly added [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] management service URL, expand **LOB Types**, right-click **SQL**, and select **Add SQL Target**.

   ![](/Image/FFBridge-AddSQLTarget.gif)

   The **Add a Target** wizard starts.

   1. Read the information on the **Before You Begin** page, and then select **Next**.

   2. On the **Connection Parameters** page, enter the details for the SQL Server to connect to and the credentials to use for the connection.

      For the **Server** field, enter the name of the computer where SQL Server is installed and for the database (**Initial Catalog**), enter **CloudCarDatabase**.

      > [!NOTE]
      > You can use the **Advanced** button to build the SQL Server connection URI and also enter the binding properties for the connection.
      > 
      > [The SQL Server Connection URI](http://go.microsoft.com/fwlink/p/?LinkId=228970) provides additional information about how to build the URI. For information about binding properties, see [Working with BizTalk Adapter for SQL Server Binding Properties](http://go.microsoft.com/fwlink/p/?LinkId=228971).
      > 
      > For this tutorial, leave the default setting as-is for the binding properties.

      Enter the credentials to connect to the SQL Server database. You must have already added that user as a system administrator in the SQL Server database.

      Select **Next**.

   3. On the **Operations** page, from the left box, expand **Tables**, expand **Orders**, select **Insert**, and then select the RIGHT ARROW. Notice that the **Insert** operation is listed under the **Selected operations** section. **Select Next**.

   4. In the **Runtime Security** page, enter the security type. This security type determines how the client message is authenticated with the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. Options include:

      |||
      |-|-|
      |Fixed Username <br /> <br />|Select this option if you are using a username and password created locally on the LOB system. <br /> <br />|
      |Fixed Windows credential <br /> <br />|Select this option to use a Windows domain account. <br /> <br />|
      |Custom SOAP Header <br /> <br />|Select this option if you create a custom SOAP header to include the username and password. <br /> <br />|
      |Message Credential <br /> <br />|Select this option if you are including the logon credentials in the WS-Security header of the message. <br /> <br />|
      For this tutorial use the **Fixed Username** option, enter the same credentials that you use to connect to the computer running SQL Server, and then select **Next**.

   5. On the **Deployment** page, choose an existing [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] or create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. To create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)], enter the following details:

      |||
      |-|-|
      |Namespace <br /> <br />|Enter the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace on which the LOB relay endpoint is created. <br /> <br />|
      |Issuer Name <br /> <br />|Enter the issuer name for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. <br /> <br />|
      |Issuer Secret <br /> <br />|Enter the issuer secret for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. <br /> <br />|
      |Relay Path <br /> <br />|Enter a name for the relay. For this tutorial, enter **SQLtarget**. <br /> <br />|
      |Target Sub-path <br /> <br />|Enter a sub-path to make this target unique. For this tutorial, enter **orders**. <br /> <br />|
      |Target runtime URL <br /> <br />|This read-only property displays the URL where the relay is deployed on [!INCLUDE[sb2](/Token/sb2_md.md)]. This is the endpoint where you can send a message with a compliant schema to be inserted into the on-premises SQL Server. <br /> <br />|
      Select **Next**.

   6. On the **Summary** page, review the values you specified in the previous steps, and then select **Create**.

   7. When the wizard completes, select **Finish**. The following activities occur in the background:

      - An [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created in Server Explorer. It can be disabled, started, and deleted. Its configuration can also be exported.

      - An [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created as an application in IIS. This application uses the Runtime for this specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) describes the IIS components.

3. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], include the schemas for the **Insert** operation on the **Orders** table. Make sure the **CloudCar_Integration_PurchaseOrder** project is selected in the Solution Explorer when you perform the following steps.

   1. Right-click the SQL [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] you created for the **Orders** table, and select the option to add schemas to the project.

   2. For **File name prefix**, enter **PO_**.

   3. Retain the folder name as **LOB Schemas**.

   4. For **Credential Type**, select **Windows**, and then select **OK**.

4. Finally, set the security property for the relay endpoint.

   1. Right-click the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] in Server Explorer and select **Properties**.

   2. In the Properties grid, select the ellipsis **(…)** against the **Runtime Security** property.

   3. In the **Edit Security** dialog box, select **Fixed Windows Credentials** and enter username and password to connect to the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)].

   4. Select **OK**.

5. Save changes to the project.

## See Also
[Create a BizTalk Service project to process purchase orders](/Topic/Create_a_BizTalk_Service_project_to_process_purchase_orders.md)

