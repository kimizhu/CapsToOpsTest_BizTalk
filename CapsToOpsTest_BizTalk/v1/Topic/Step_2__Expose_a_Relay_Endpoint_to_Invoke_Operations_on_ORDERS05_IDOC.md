---
description: na
keywords: na
pagetitle: Step 2: Expose a Relay Endpoint to Invoke Operations on ORDERS05 IDOC
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.service: multiple
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c18c624c-978c-4476-8f03-5caa7b12e103
---
# Step 2: Expose a Relay Endpoint to Invoke Operations on ORDERS05 IDOC
There are two main steps required to expose an SAP artifact as an operation that can be invoked by sending a message over [!INCLUDE[sb2](/Token/sb2_md.md)] – create an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] and an [!INCLUDE[lobrelay](/Token/lobrelay_md.md)].

- An [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] defines how an [!INCLUDE[azure_2](/Token/azure_2_md.md)] application communicates to the Line-of-Business (LOB) system. The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] controls the LOB system connection URI, the operation to perform, and the connection credentials.

- An [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] is a WCF service running within an organizations firewall and listens to a relay endpoint on the [!INCLUDE[sb2](/Token/sb2_md.md)]. As the name suggests, the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] acts as a relay between the [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint and the LOB system. It receives the message at the [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint and passes it on to the relevant LOB system using the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] configuration.

For more information, see [BizTalk Adapter Service Architecture](http://go.microsoft.com/fwlink/p/?LinkId=241590). In this topic, we create an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] and an [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to expose the **Send** operation on the ORDERS05 IDOC.

### To create an LOB Target and LOB Relay

1. Open Visual Studio (as an administrator), create a new **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]**, and name it **SAPIntegration**.

2. You first start with adding a [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] server. This is the server where you installed the Runtime component of [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]. To add a [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] server, from the Server Explorer in Visual Studio, right-click **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**s, and select **Add [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**. In the **Add [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** dialog box, enter the URL of the WCF service that monitors that [!INCLUDE[sb2](/Token/sb2_md.md)] relay service, and then select **OK**:

   ![](/Image/AFINT_PG_AddSBServer.gif)

   Because you have all the components of [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] installed on the same computer, the URL for that service will be `http://localhost:8080/BAService/ManagementService.svc/`.

   > [!NOTE]
   > If you had installed [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime component on a separate computer, you replace ‘localhost’ in the above URL with the name of that computer.

3. In this tutorial, we are creating an application to integrate with SAP, so we must add an SAP target. Expand the newly added server, expand **LOB Types**, right-click **SAP**, and select **Add SAP Target**:

   ![](/Image/AFINT_PG_AddSAPTarget.gif)

   The **Add a Target** wizard starts. Perform the following steps to create an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)].

   1. Read the information on the **Before You Begin** page, and then select **Next**.

   2. On the **Connection Parameters** page, specify the details for the SAP Server to connect to and the credentials to use for the connection. Select **Next**.

   3. On the **Operations** page, expand the **ORDERSO5** IDOC category (under \IDOC\ORDERS\). There are several versions of the IDOC available. For this tutorial, we’ll select **ORDERS05.V3(700)**. Expand this IDOC, select **Send**, and then select the right arrow to add it to the **Selected Operations** box:

      ![](/Image/AFINT_PG_AddSendOp.gif)

      Select **Next**.

   4. In the **Runtime Security** page, specify the security mechanism to be used by the LOB Server to authenticate the target resource when a message arrives from a client. For this tutorial, select **Fixed Username** and specify the credentials to connect to the SAP server.

   5. On the **Deployment** page, you create an [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] and an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to provide connectivity to your on-premise LOB applications from the cloud.

      Select the **Create new** option to create a new relay and provide the following values:

      |Name <br /> <br />|Description <br /> <br />|
      |--------|---------------|
      |Namespace <br /> <br />|Specify the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace on which the LOB relay endpoint is created. <br /> <br />|
      |Issuer name <br /> <br />|Specify the issuer name for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|
      |Issuer secret <br /> <br />|Specify the issuer secret for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|
      |Relay path <br /> <br />|Specify a name for the relay. For this tutorial, enter **sapintegration01**. <br /> <br />|
      |Target sub-path <br /> <br />|Enter a sub-path to make this target unique. For this tutorial, enter **orders**. <br /> <br />|
      The **Target runtime URL** read-only property displays the URL where the relay is deployed on [!INCLUDE[sb2](/Token/sb2_md.md)]. This is the path where you could send a message to be inserted into the on-premises SAP Server. In our scenario, this is where the [!INCLUDE[bridge](/Token/bridge_md.md)] sends the message.

      Select **Next**.

   6. On the **Summary** page, review the values you specified in the previous steps, and then select **Create**.

   7. When the wizard completes, select **Finish**.

      In Visual Studio Server Explorer, you now have an entry under the **SAP** node. This represents the relay endpoint created in [!INCLUDE[sb2](/Token/sb2_md.md)] to relay PO messages coming from the cloud to the on-premises SAP system.

### To add schemas

1. After adding the relay endpoint to an SAP system, you must add schemas that to send ORDERS05 PO messages to the SAP server. To add the schemas, right-click the relay endpoint and select **Add schemas to SAPIntegration**. In the dialog box, do the following:

   - Enter a filename prefix that will be included in the name of each schema file that is generated. For this tutorial, specify this as **SAPIntegration_**.

   - Enter a folder name that will be added to your solution under which all the schemas will be added. For this tutorial, specify the folder name as **LOB Schemas**.

   - Enter the credentials to connect to an SAP system.

   ![](/Image/AFINT_PG_AddSchemas.gif)

   Select **OK**. The schemas are added to the project under an **LOB Schemas** folder.

### To use the LOB Target

1. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties** and update the **BizTalk Service URL** property to include your [!INCLUDE[af_integration](/Token/af_integration_md.md)] name. This is the name that you provided in [Azure classic portal](http://go.microsoft.com/fwlink/?LinkId=517414) while provisioning the [!INCLUDE[af_integration](/Token/af_integration_md.md)].

2. Set the security property for the relay endpoint:

   1. Right-click the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] in Server Explorer and select **Properties**.

   2. In the Properties grid, select the ellipsis **(…)** against the **Runtime Security** property.

   3. In the **Edit Security** dialog box, select **Fixed Username**, and enter the username and password to connect to the SAP Server.

   4. Select **OK**.

3. Drag and drop the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] onto the design area. Note the **Entity Name** property of the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. The default value is *Relay-Path_target-sub-path*. If using the examples above, it is *sapintegration01_orders*.

4. Open the .config file for the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)], which typically has the naming convention as *YourRelayPath_target-sub-path.config*. Specify the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name and issuer secret, as shown below:

   ```
   <tokenProvider>
     <sharedSecret issuerName="owner" issuerSecret="issuer_secret" />
   </tokenProvider>
   ```
   Save changes to the config file.

## See Also
[Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server](/Topic/Tutorial__Using_Azure_BizTalk_Services_to_Integrate_with_an_On-Premises_SAP_Server.md)

