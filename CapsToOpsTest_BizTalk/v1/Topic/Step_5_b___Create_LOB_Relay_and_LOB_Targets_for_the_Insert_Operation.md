---
description: na
keywords: na
pagetitle: Step 5(b): Create LOB Relay and LOB Targets for the Insert Operation
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cddce78-b5ca-4f6f-ba6c-d1ba7b7cfcf2
---
# Step 5(b): Create LOB Relay and LOB Targets for the Insert Operation
There are two main steps for exposing an SQL Server table operation as an operation that can be invoked by sending a message over [!INCLUDE[sb2](/Token/sb2_md.md)] – create an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] and an [!INCLUDE[lobrelay](/Token/lobrelay_md.md)].

- An [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] defines how an Azure application communicates to the Line-of-Business (LOB) system. The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] controls the LOB system connection URI, the operation to perform, and the connection credentials.

- An [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] is a WCF service that runs within an organizations firewall and listens to a relay endpoint on the [!INCLUDE[sb2](/Token/sb2_md.md)]. As the name suggests, the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] acts as a relay between the [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint and the LOB system. It receives the message at the [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint and passes it on to the relevant LOB application by using the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] configuration.

For more information, see [BizTalk Adapter Service Architecture](http://go.microsoft.com/fwlink/p/?LinkId=241590). This topic demonstrates how to create an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] and an [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to expose the **Insert** operation on the **Claims** table in the SQL Server database.

### To create an SQL Server [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]

1. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], open **Server Explorer**, right-click **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**, and then select **Add Server**. In the dialog box that pops up, enter the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management URL. The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management URL is path to the ManagementService.svc WCF service hosted in IIS. This management service monitors the [!INCLUDE[sb2](/Token/sb2_md.md)] relay service hosted on [!INCLUDE[azure_1](/Token/azure_1_md.md)]. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) provides more information on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] components within IIS.

   ![](/Image/AFINT_PG_AddSBServer.gif)

   Because you have all the components – [!INCLUDE[af_integration](/Token/af_integration_md.md)] as well as [!INCLUDE[lobconnect](/Token/lobconnect_md.md)], installed on the same computer, the URL for that service will be `http://localhost:8080/BAService/ManagementService.svc/`.

   > [!NOTE]
   > If you had installed [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime component on a separate computer, you would have replaced ‘localhost’ in the above URL with the name of that computer.

   Click **OK**.

2. Expand the newly added server, expand **LOB Types**, right-click **SQL**, and select **Add SQL Target**.

   ![](/Image/FFBridge-AddSQLTarget.gif)

   The **Add a Target** wizard starts.

   1. Read the information on the **Before You Begin** page, and then click **Next**.

   2. On the **Connection Parameters** page, enter the details for the SQL Server to connect to and the credentials to use for the connection. Click **Next**.

      > [!NOTE]
      > You can use the **Advanced** button to build the SQL Server connection URI and also enter the binding properties for the connection.
      > 
      > [The SQL Server Connection URI](http://go.microsoft.com/fwlink/p/?LinkId=228970) provides additional information about how to build the URI. For information about binding properties, see [Working with BizTalk Adapter for SQL Server Binding Properties](http://go.microsoft.com/fwlink/p/?LinkId=228971).
      > 
      > For this tutorial, leave the default setting as-is for the binding properties.

   3. On the **Operations** page, from the left box, expand **Tables**, expand **Claims**, select **Insert**, and then click the RIGHT ARROW. Notice that the **Insert** operation is listed under the **Selected operations** section.

      ![](/Image/FFBridge-SelectSQLOp.gif)

      Click **Next**.

   4. In the **Runtime Security** page, enter the security type. This security type determines how the client message is authenticated with the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. Options include:

      |||
      |-|-|
      |Fixed Username <br /> <br />|Select this option if you are using a username and password created locally on the LOB system. <br /> <br />|
      |Fixed Windows credential <br /> <br />|Select this option to use a Windows domain account. <br /> <br />|
      |Custom SOAP Header <br /> <br />|Select this option if you create a custom SOAP header to include the username and password. <br /> <br />|
      |Message Credential <br /> <br />|Select this option if you are including the logon credentials in the WS-Security header of the message. <br /> <br />|
      For this tutorial use the **Fixed Windows credential** option, enter the credentials, and then click **Next**.

   5. On the **Deployment** page, choose an existing [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] or create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)].

      > [!TIP]
      > A single [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] can be used with multiple [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. There are some restrictions based on the security model. As a best practice, group the same security method in one [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. For example, use the same [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to host the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s that use Message Credential or Fixed Windows security type.

      To create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)], enter the following details:

      |||
      |-|-|
      |Namespace <br /> <br />|Enter the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace on which the LOB relay endpoint is created. <br /> <br />|
      |Issuer Name <br /> <br />|Enter the issuer name for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|
      |Issuer Secret <br /> <br />|Enter the issuer secret for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|
      |Relay Path <br /> <br />|Enter a name for the relay. For this tutorial, enter **SQLLOBRelay**. <br /> <br />|
      |Target Sub-path <br /> <br />|Enter a sub-path to make this target unique. For this tutorial, enter **Claims**. <br /> <br />|
      |Target runtime URL <br /> <br />|This read-only property displays the URL where the relay is deployed on [!INCLUDE[sb2](/Token/sb2_md.md)]. This is the path where you could send a message to be inserted into the on-premises SQL Server. In our scenario, this is where the [!INCLUDE[bridge](/Token/bridge_md.md)] routes the message. <br /> <br />|
      Click **Next**.

   6. On the **Summary** page, review the values you specified in the previous steps, and then click **Create**.

   7. When the wizard completes, click **Finish**. The following activities occur in the background:

      - An [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created in Server Explorer. It can be disabled, started, and deleted. Its configuration can also be exported.

      - An [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created as an application in IIS. This application uses the Runtime for this specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) describes the IIS components.

3. Save changes to the project.

### To use the LOB Target

1. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface, select **Properties** and verify that the **BizTalk Service URL** property is updated to include your [!INCLUDE[af_integration](/Token/af_integration_md.md)] name. This is the name that you provided in [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414) while provisioning the [!INCLUDE[af_integration](/Token/af_integration_md.md)].

2. Set the security property for the relay endpoint.

   1. Right-click the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] in Server Explorer and select **Properties**.

   2. In the Properties grid, click the ellipsis **(…)** against the **Runtime Security** property.

   3. In the **Edit Security** dialog box, select **Fixed Windows Credentials** and enter the username and password to connect to the SQL Server.

   4. Click **OK**.

3. Drag and drop the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] onto the design surface. Note the **Entity Name** property of the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. The default value is *Relay-Path_target-sub-path*. If using the examples above, it will be *&#42;sqllobrelay_claims&#42;*.

4. Open the .config file for the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)], which typically has the naming convention as *YourRelayPath_target-sub-path.config*. Enter the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name and issuer secret, as shown below:

   ```
   <tokenProvider>
     <sharedSecret issuerName="owner" issuerSecret="<issuer_secret>" />
   </tokenProvider>
   ```
   Save changes to the config file.

## See Also
[Step 5: Create and Configure the LOB Target](/Topic/Step_5__Create_and_Configure_the_LOB_Target.md)

