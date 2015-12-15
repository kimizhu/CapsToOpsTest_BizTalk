---
description: na
keywords: na
pagetitle: Create a SQL Server LOB target to insert invoice
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 713e93af-8273-40f6-9de2-0e512502573f
---
# Create a SQL Server LOB target to insert invoice
This topic provides instructions on how to create an SQL Server [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] within the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. You use this [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to insert invoice data into the **Invoice** table in the **CloudCarDatabase**. You must have already created the database and the table by using the **CreateDatabaseSchema_CloudCar.sql** script provided with the sample available in the MSDN code gallery at [http://go.microsoft.com/fwlink/p/?LinkId=324220](http://go.microsoft.com/fwlink/p/?LinkId=324220).

### To create an SQL Server LOB target

1. From the Server Explorer, expand the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] management service URL, expand **LOB Types**, right-click **SQL**, and select **Add SQL Target**.

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

      Specify the credentials to connect to the SQL Server database. You must have already added that user as a system administrator in the SQL Server database.

      Click **Next**.

   3. On the **Operations** page, from the left box, expand **Tables**, expand **Invoice**, select **Insert**, and then select the RIGHT ARROW. Notice that the **Insert** operation is listed under the **Selected operations** section. **Select Next**.

   4. In the **Runtime Security** page, enter the security type. This security type determines how the client message is authenticated with the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. Options include:

      |||
      |-|-|
      |Fixed Username <br /> <br />|Select this option if you are using a username and password created locally on the LOB system. <br /> <br />|
      |Fixed Windows credential <br /> <br />|Select this option to use a Windows domain account. <br /> <br />|
      |Custom SOAP Header <br /> <br />|Select this option if you create a custom SOAP header to include the username and password. <br /> <br />|
      |Message Credential <br /> <br />|Select this option if you are including the logon credentials in the WS-Security header of the message. <br /> <br />|
      For this tutorial use the **Fixed Username** option, specify the same credentials that you use to connect to the computer running SQL Server, and then select **Next**.

   5. On the **Deployment** page, choose an existing [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] or create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)].

      > [!TIP]
      > A single [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] can be used with multiple [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. There are some restrictions based on the security model. As a best practice, group the same security method in one [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. For example, use the same [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to host the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s that use Message Credential or Fixed Windows security type.

      In the step [Create a SQL Server LOB target to insert purchase order](/Topic/Create_a_SQL_Server_LOB_target_to_insert_purchase_order.md), we already created an [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to insert purchase order messages into the **CloudCarDatabase**. We can use the same [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to insert the invoice data as well. Select the option to use existing relay and then select **cloudcarsb/sqltarget**. Even though you use an existing relay, you must enter a target sub-path to make the target unique. For this tutorial, for creating SQL [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to write to the Invoice table, enter the **Target Sub-path** as **invoice**.

      Click **Next**.

   6. On the **Summary** page, review the values you specified in the previous steps, and then select **Create**.

   7. When the wizard completes, click **Finish**.

2. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], include the schemas for the **Insert** operation on the **Invoice** table. Make sure the **CloudCar_Integration_Invoice** project is selected in the Solution Explorer when you perform the following steps.

   1. Right-click the SQL [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] you created for the **Invoice** table, and select the option to add schemas to the project.

   2. For **File name prefix**, enter **Invoice_**.

   3. Retain the folder name as **LOB Schemas**.

   4. For **Credential Type**, select **Windows**, and then select **OK**.

3. Finally, set the security property for the relay endpoint.

   1. Right-click the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] in Server Explorer and select **Properties**.

   2. In the Properties grid, select the ellipsis **(…)** against the **Runtime Security** property.

   3. In the **Edit Security** dialog box, select **Fixed Windows Credentials** and enter username and password to connect to the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)].

   4. Click **OK**.

4. Save changes to the project.

## See Also
[Create a BizTalk Service project to process invoices](/Topic/Create_a_BizTalk_Service_project_to_process_invoices.md)

