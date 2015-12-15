---
description: na
keywords: na
pagetitle: Connect to Oracle Database or eBusiness Suite in a BizTalk Services Project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a125135-fcc4-42c0-8c39-857412c99958
---
# Connect to Oracle Database or eBusiness Suite in a BizTalk Services Project
There are three overall steps to connect to an Oracle database or Oracle eBusiness Suite application from a [!INCLUDE[af_integration](/Token/af_integration_md.md)] project.

- Create an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] for Oracle.

   > [!IMPORTANT]
   > - To create an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] for Oracle, you must be a member of the local Administrators group and have the System Administrator right on the on-premises Oracle system.
   > - Visual Studio must be opened with Administrative privileges to use [!INCLUDE[lobconnect](/Token/lobconnect_md.md)].

- Use the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]

- Generate schema for the operation to be performed on Oracle.

> [!IMPORTANT]
> These steps assume you have a [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md) lists the requirements.

### To add an [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] for Oracle

1. In Server Explorer, expand **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**, expand the Management URL, and then expand **LOB Types**.

2. Right-click **Oracle DB** or **Oracle EBS** and select **Add Oracle Target**. The **Add a Target** wizard opens:

   1. In the Welcome window, select **Next**.

   2. In Connection Parameters, enter the following:

      - **Server**: The server name or IP address of the Oracle system and optionally, the port number. If the port number is not entered, port 1521 is used. To use a different port, enter *ComputerName:PortNumber*.

      - **Service Name**: Required when Server is specified.

      - **Advanced**: Select this button to configure additional Connection Properties and any Binding Properties:

         |||
         |-|-|
         |Port Number <br /> <br />|**Required**. Default is 1521, which is the typical Net Listener for Oracle. <br /> <br />|
         |ServerAddress <br /> <br />|**Required**. The name or the IP address of the Oracle server. <br /> <br />|
         |ServiceName <br /> <br />|**Optional**. The name of the Oracle service. <br /> <br />|
         |ServiceType <br /> <br />|**Required**. Default is **Dedicated**. Options include: <br /> <br />Dedicated <br /> <br />Uses a single server process to serve a single user process. <br /> <br />Shared <br /> <br />Uses a shared server process that can that can serve multiple user processes. <br /> <br />|
         |DataSourceName <br /> <br />|**Optional**: The Oracle Transparent Network Substrate (TNS) network alias. <br /> <br />If specifying the ServerAddress and ServiceName, do not enter a DataSource. If not specifying the ServerAddress and ServiceName, enter a DataSource. **Important:** The TNS network alias may be case-sensitive. <br />|
         In the **Binding Properties** tab, refer to [Working with BizTalk Adapter for Oracle Database Binding Properties](http://go.microsoft.com/fwlink/p/?LinkId=228967) or [Working with BizTalk Adapter for Oracle E-Business Suite Binding Properties](http://go.microsoft.com/fwlink/p/?LinkId=228984).

         [The Oracle Database Connection URI](http://go.microsoft.com/fwlink/p/?LinkId=228966) and [The Oracle E-Business Suite Connection URI](http://go.microsoft.com/fwlink/p/?LinkId=228983) provide additional information.

      - **Specify the credentials**: Enter the credentials to authenticate to the on-premises Oracle system. Options include:

         |||
         |-|-|
         |Use Windows Credentials <br /> <br />|The logged on user credentials are used to connect to the Oracle system. <br /> <br />|
         |Use the following UserName and Password: <br /> <br />|Enter a **User name** and **Password** that can connect to the Oracle system. **Important:** User names in Oracle are case-sensitive. For release 10g and earlier, passwords on the Oracle system are not case-sensitive. <br />|
         > [!NOTE]
         > Not all options may be available for this LOB adapter.

         Select **Next**.

   3. In Operations, expand the node, select the database operations, and select the right arrow:

      ![](/Image/AI_AddOracleLob.gif)

      [Browsing, Searching, and Retrieving Metadata for Oracle Operations](http://go.microsoft.com/fwlink/p/?LinkId=228968) and [Browsing, Searching, and Retrieving Metadata for Oracle E-Business Suite Operations](http://go.microsoft.com/fwlink/p/?LinkId=228985) provide additional details on selecting an operation.

      To see the operation’s generated WSDL, select the operation, and select **Properties**.

      Select **Next**.

   4. In Runtime Security, enter the security type. This security type determines how the client message is authenticated with the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. Options include:

      |||
      |-|-|
      |Fixed username <br /> <br />|Select this option if you are using a username and password created locally on the LOB system. <br /> <br />|
      |Custom SOAP Header <br /> <br />|Select this option if you create a custom SOAP header to include the username and password. <br /> <br />|
      |Message Credential <br /> <br />|Select this option if you are including the logon credentials in the WS-Security header of the message. <br /> <br />|
      Select **Next**.

   5. In Deployment, choose an existing [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] or create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)].

      > [!TIP]
      > A single [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] can be used with multiple [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. There are restrictions based on the security model. As a best practice, group the same security method in one [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. For example, use the same [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to host the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s that use the Message Credential or Fixed Windows credential security type.

      To create a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]:

      |||
      |-|-|
      |Namespace <br /> <br />|**Required**. Enter your [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. The namespace name is available in the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414). <br /> <br />|
      |Issuer Name <br /> <br />|**Required**. A valid [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name is required. <br /> <br />|
      |Issuer Secret <br /> <br />|**Required**. A valid [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Secret key is required. <br /> <br />|
      |Relay Path <br /> <br />|**Required**. Enter the desired name of the relay path. For example, if you use chose Fixed Windows credential option for Runtime Security, you can enter something like *WindowsAuthRelay*. <br /> <br />|
      |Target Sub-path <br /> <br />|**Required**. Enter a sub-path to make this target unique. For example, you can enter *GetOrder*. <br /> <br />|
      |Target runtime URL <br /> <br />|This is automatically populated with the namespace name, relay path and target sub-path specified. If using the examples above, it is populated with something like: <br /> <br />`https://MyNamespace.servicebus.windows.net/WindowsAuthRelay/GetOrder` <br /> <br />|
      Select **Next**.

   6. Summary shows your configured values. Select **Create**.

   7. When complete, select **Finish**.  The following activities occur in the background:

      - The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created in Server Explorer. It can be disabled, started, and deleted. Its configuration can also be exported.

      - The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created as an application in IIS. This application uses the Runtime for this specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) describes the IIS components.

### To use the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]

1. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**, and update the **BizTalk Service URL** property to include your [!INCLUDE[af_integration](/Token/af_integration_md.md)] name. This is the name that you entered in [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414) when creating the [!INCLUDE[af_integration](/Token/af_integration_md.md)].

2. Set the security property for the relay endpoint:

   1. Right-click the relay endpoint in Server Explorer, and select **Properties**.

   2. In the Properties grid, select the ellipsis **(…)** next to the **Runtime Security** property.

   3. In the **Edit Security** dialog box, select the security method you want to use, and enter their values.

   4. Select **OK**.

3. Drag and drop the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] onto the design area. Note the **Entity Name** property of the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. The default value of the property is *Relay-Path_target-sub-path*.

4. Open the .config file for the LOB target, which typically has the *RelayPath_target-sub-path.config* naming convention. Enter the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name and issuer secret, as shown:

   ```
   <tokenProvider>
     <sharedSecret issuerName="owner" issuerSecret="issuer_secret" />
   </tokenProvider>
   ```
   Save changes to the config file.

Once a [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is configured and added to the design area, add a [!INCLUDE[one-way](/Token/one-way_md.md)] or a [!INCLUDE[request_response](/Token/request_response_md.md)] to be the source. Use **Connector** in the Toolbox to connect the [!INCLUDE[bridge](/Token/bridge_md.md)] to the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)], similar to the following:

![](/Image/AI_MFConnectionLOB.jpg)

[Create an XML One-Way Bridge](/Topic/Create_an_XML_One-Way_Bridge.md) and [Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md) provide more specific information on the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] and any additional properties that must be configured.

> [!TIP]
> The [!INCLUDE[bridge](/Token/bridge_md.md)] uses the **Relative Address** property of the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] to send messages to the on-premises LOB system.

### To generate the schema

1. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], in the **Server Explorer**, right click the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] you created, and then select **Add schemas to &#42;&lt;project_name&gt;&#42;**. The **Schema Generation** dialog opens.

2. Enter a file name prefix. This value is prefixed with all the schema files that are generated. You can also enter the folder name under which the schemas are added in the Visual Studio Solution Explorer. The default value for the folder is **LOB Schemas**.

3. Select a credential type to generate the schema, provided appropriate values for authentication, and then select **OK**.

   The schemas are added to the project under the folder name.

## See Also
[Connect to mySAP Business Suite in a BizTalk Services Project](/Topic/Connect_to_mySAP_Business_Suite_in_a_BizTalk_Services_Project.md)
[Connect to SQL Server in a BizTalk Services Project](/Topic/Connect_to_SQL_Server_in_a_BizTalk_Services_Project.md)
[Connect to Siebel eBusiness Applications in a BizTalk Services Project](/Topic/Connect_to_Siebel_eBusiness_Applications_in_a_BizTalk_Services_Project.md)
[PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md)
[Connect to LOB systems from a BizTalk Services Project](/Topic/Connect_to_LOB_systems_from_a_BizTalk_Services_Project.md)

