---
description: na
keywords: na
pagetitle: Configure EDI Send bridge settings in BizTalk Services Portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6872b02d-114f-4271-bc90-ce9df470ce97
---
# Configure EDI Send bridge settings in BizTalk Services Portal
Configure the EDI Send Bridge settings in the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal.

The EDI send bridge configuration includes settings such as the endpoint where EDI messages must be sent, any transforms to use while processing the message, and transport settings.

## Configure the Inbound URL
The inbound URL determines the input endpoint URL to send messages to the EDI send bridge. You can also use this page to promote properties from the incoming SOAP or HTTP message headers; which can be later used for batching configuration.

1. On the **Inbound URL** page of the **Send Settings** tab, the **Endpoint** URL is automatically populated with the address used to input messages to the send pipeline. You can only edit the GUID in the URL and provide a unique value. A message sent to this URL is processed by the bridge and then sent to the guest trading partner.

2. Expand **Promoted Properties** and then select the (**+**) sign to promote a property. The following table details the required fields and the values:

   |Field <br /> <br />|Description <br /> <br />|
   |---------|---------------|
   |Source Type <br /> <br />|Select the message type from which the header values are extracted. For assigning header values to properties, the possible values are **SOAP** and **HTTP**. <br /> <br />|
   |Property Name <br /> <br />|Enter the name of the property that you are defining. For example, you can set this to **MsgType**. <br /> <br />|
   |Identifier <br /> <br />|Enter the name of property present in the message header, the value of which you want to extract and assign to a property that you are defining. You can also promote the value of custom header properties. For example, in the following excerpt, **MessageType** is a custom header. <br /> <br />DELTED CODE <br /> <br />So, if you set the Identifier property **MessageType**, then the value of the header from the incoming message is extracted and is assigned to the **MsgType** property that you are defining as part of the agreement. <br /> <br />|
   |Namespace <br /> <br />|Specify the SOAP header namespace. Going by the excerpt used above, the namespace for the **MessageType** custom header is highlighted. <br /> <br />DELTED CODE <br /> <br />You do not need to provide a namespace if you are promoting a property from an HTTP message header. <br /> <br />|

## Configure the Transform
On the **[!INCLUDE[transform](/Token/transform_md.md)]** page, you can do the following:

- Upload an existing [!INCLUDE[transform](/Token/transform_md.md)] to map the incoming message to another message structure. See [Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md) to create a [!INCLUDE[transform](/Token/transform_md.md)].

- If the [!INCLUDE[transform](/Token/transform_md.md)] uses a C# Scripting [!INCLUDE[mapop](/Token/mapop_md.md)], then you can upload the required assemblies as part of the agreement.

- Finally, you can promote properties on the incoming message based on XPath and Lookup queries.

### Add a transform

1. If a transform is already uploaded to your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription, then select (**+**), and select the [!INCLUDE[transform](/Token/transform_md.md)] from the drop-down.

   If the [!INCLUDE[transform](/Token/transform_md.md)] is not already uploaded, then:

   1. Select **Upload** and browse for the [!INCLUDE[transform](/Token/transform_md.md)] to use.

   2. In the Open dialog box, select the [!INCLUDE[transform](/Token/transform_md.md)] file, and select **Open**. [!INCLUDE[transform](/Token/transform_md.md)] files are saved with a .trfm extension.

   3. The selected [!INCLUDE[transform](/Token/transform_md.md)] is added to the list of [!INCLUDE[transform](/Token/transform_md.md)]s.

2. If the [!INCLUDE[transform](/Token/transform_md.md)] you uploaded includes a scripting [!INCLUDE[mapop](/Token/mapop_md.md)], expand the **Assembly** section, and select **Upload** to browse to upload the assembly required for the scripting [!INCLUDE[mapop](/Token/mapop_md.md)].

### Add an assembly
If the [!INCLUDE[transform](/Token/transform_md.md)] you are using includes an external file assembly (.dll), upload it to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

1. Expand the **Assembly** section.

2. Select **Upload** to browse to the .dll assembly.

## Promote a Property
Expand the **Promoted Properties** section. The following options are available:

### <a name="BKMK_SendXPath"></a>Promote a property using XPath queries

1. On the **[!INCLUDE[transform](/Token/transform_md.md)]s** page, expand the **XPath** section.

2. For the **Property Name** field, enter the name of the property that you are defining. The value of this property is set to the value that is extracted from the message body using the XPath query.

3. For the **Schema** field, from the drop-down select the schema for the incoming message. If the schema is not already available, you can upload it using the **Upload** button.

4. For the **XPath** field, specify the XPath query to extract an element or an attribute from a message. A typical XPath query would look like the following:

   ```
   /*[local-name()='<root_node>' and namespace-uri()='<namespace>']/*[local-name()='<node_name>' and namespace-uri()=<namespace>']/*@[local-name()='<attribute_name>' and namespace-uri()='<namespace>']
   ```
   > [!TIP]
   > You can get an XPath query from the schema editor. In the Schema Editor available as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], select the schema element for which you want the XPath querty, and in the Properties window look for the value of the **Instance Xpath** property. That should be the XPath query for the node.

### <a name="BKMK_SendLookup"></a>Promote a property using Lookup

1. On the **[!INCLUDE[transform](/Token/transform_md.md)]s** page, expand the **Lookup** section.

2. For the **Property Name** field, enter the name of the property that you are defining. The value of this property is set to the value that is extracted using the lookup configuration you are defining.

3. For the **Connection URL** field, provide a valid connection URL to connect to a [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)].

4. For the **Table Name** field, enter the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table name from which you want to do a data lookup.

5. For the **Query Out Column** field, enter a column name in the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table, the value of which is the output value that is eventually assigned to the looked up property.

6. For the **Query In Column** field, enter a column name in the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table, the values of which are used as the input query for performing the data lookup.

7. From the **Input Property** drop-down list, select a property that you must have already defined. The value of this property is passed on to the **Query In Column** specified earlier.

Let us now understand how the lookup configuration is used at run-time. To understand this better, let us assume a table (**TempTable**) exists in [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)]. This table has two columns, **PurchaseOrder** and **CustomerName**. Let us also assume that you already promoted a property called **P1** as part of the agreement.

|||
|-|-|
|PropertyName <br /> <br />|**P2**. This is the property that will contain the value promoted using a lookup configuration. <br /> <br />|
|TableName <br /> <br />|**TempTable** <br /> <br />|
|Query In Column <br /> <br />|**PurchaseOrder** <br /> <br />|
|Query Out Column <br /> <br />|**CustomerName** <br /> <br />|
|Input Query <br /> <br />|**P1**. You could have promoted this property earlier either using XPath or from the SOAP or HTTP message header. Let us assume the value of P1, at runtime, is set to **PO1234**. <br /> <br />|
This is how the configuration is used:

- The agreement looks up the value of P1 (**PO1234**) in the input query column (**PurchaseOrder**) in the table (**TempTable**).

- The agreement then picks up the value corresponding to **PO1234** from the output query column (**CustomerName**) in the **TempTable**.

- The value picked up from the output query column is assigned to the property P2. For example, if the customer name corresponding to purchase order **PO1234** is **John**, then the value of P2 is set to John.

## Configure the transport
On this page, you enter the transport settings used for sending messages from the hosting partner to the guest partner. If the hosted partner requests an acknowledgement, the acknowledgement is received by the hosting partner based on the settings configured in the **Receive Settings** tab. You can do the following on the **Transport** tab:

- Set route conditions/rules based on which messages are routed to destination endpoints.

- Set route actions. Route actions can be used to include specific message headers (for SOAP and HTTP) before the message is sent to the destination endpoint.

- Set route destinations for messages that are successfully processed or get suspended.

- Set message suspensions settings for routing a suspended message to a [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)], [!INCLUDE[azure_2](/Token/azure_2_md.md)] Blobs, or [!INCLUDE[azure_2](/Token/azure_2_md.md)][!INCLUDE[sb2](/Token/sb2_md.md)].

### Transport Settings

1. On the **Route** page of the **Receive Settings** tab, expand **Route Settings**, and then click **Add**.

2. In the dialog box that pops us, you specify three key routing configurations – routing condition, routing action, and routing destination.

   1. Specify a unique name for the routing rule.

   2. **Route Rule**: Specify the routing condition based on the properties you promoted earlier. You can either use the grid to specify the condition or provide a SQL 92 filter expression that specifies the condition. To understand this better, let us assume you promoted a property (**CustName**) whose value is set to **John** at runtime. To use this property as a routing condition, you can do either of the following:

      - Select the option for the grid, and then click the (**+**) icon to select the property you promoted. From the grid, select **CustName**, specify the **Operation** as (**==**), and set the value to **John**.

         OR

      - Select the **Use advanced definitions** option, and specify a SQL 92 expression, such as:

         ```
         CustName == ‘John’
         ```
         You can use this option to provide more detailed query expressions using other operators as well.

   3. **Route action**: If the route condition is met, at runtime the agreement stamps message headers based on the route actions you specify here. Under **Route action**, click the (**+**) icon, and specify the following values.

      |Field Name <br /> <br />|Description <br /> <br />|
      |--------------|---------------|
      |Target Type <br /> <br />|Set this to SOAP or HTTP. <br /> <br />|
      |Header <br /> <br />|Specifies the name of message header property to which a value will be assigned. You can also specify custom headers here. <br /> <br />|
      |Namespace <br /> <br />|Specify the namespace of the SOAP header to which the value will be assigned. This field is disabled if you set the **Target Type** to **HTTP**. <br /> <br />|
      |Value Type <br /> <br />|Select **Constant** if you want to assign a constant value to the header property. Select **PromotedProperty** if you want to the value of a promoted property to the header property. <br /> <br />|
      |Constant Value <br /> <br />|If you set **Value Type** to **Constant**, specify the constant value that must be assigned to the message header property. <br /> <br />|
      |Promoted Property <br /> <br />|If you set **Value Type** to **PromotedProperty**, selected the property whose value is assigned to the message header property. <br /> <br />|

   4. **Route destination**: Specify the destination where the messages are routed once they are processed by the agreement:

      > [!NOTE]
      > Even if you do not specify a routing condition and a routing action, you must specify a routing destination.

      |||
      |-|-|
      |**Azure BizTalk Bridge** <br /> <br />|Enter the name of the [!INCLUDE[bridge](/Token/bridge_md.md)] to route the message. <br /> <br />The URL looks similar to the following: <br /> <br />https://*YourDeployment*.biztalk.windows.net/default/*BridgeName* <br /> <br />|
      |**Azure Blobs** <br /> <br />|Enter the **Shared Access Signature URL** to your [!INCLUDE[azure_2](/Token/azure_2_md.md)] Blob. For example, enter: <br /> <br />https://*myAccount*.blob.core.windows.net/*ContainerName*/*BlobName**PolicyIndentifier**Signature* <br /> <br />[Managing Access to Containers, Blobs, Tables, and Queues](http://go.microsoft.com/fwlink/p/?LinkID=273871) provides more information on the **Shared Access Signature URL**. <br /> <br />|
      **Azure [!INCLUDE[sb2](/Token/sb2_md.md)]**

      You can route to any of the following [!INCLUDE[sb2](/Token/sb2_md.md)] entities.

      |||
      |-|-|
      |**Queue** <br /> <br />|Provide either the Shared Access Signature (SAS) or the shared secret for the queue. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the queue to route to. </li><li>If you choose the shared secret name, provide the URL for the queue, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>|
      |**Topic** <br /> <br />|Provide either the Shared Access Signature (SAS) or the shared secret for the topic. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the topic to route to. </li><li>If you choose the shared secret name, provide the URL for the topic, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>|
      |**BasicHttpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
      |**WebHttpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
      |**NetTcpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
      > [!IMPORTANT]
      > If you choose to route to a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, make sure the relay endpoint hosts a two-way relay service. You cannot use EDI pipelines to route to a one-way relay service.

      **FTP/S**

      Provide the following values to route to an FTP server:

      |FTP Receive Setting <br /> <br />|Description <br /> <br />|
      |-----------------------|---------------|
      |FTP server address <br /> <br />|**Required**. The FTP server address that contains the messages. The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] looks for new messages dropped to a file location this server. <br /> <br />|
      |Port number <br /> <br />|This setting determines what port the FTP server is configured to use. The default port is port 21. <br /> <br />|
      |Username <br /> <br />|If the FTP server requires authentication, enter the username that the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] uses to connect to a file location on the FTP server. <br /> <br />|
      |Password <br /> <br />|Enter the password for the username. <br /> <br />|
      |Confirm password <br /> <br />|Re-enter the username password for the FTP server. <br /> <br />|
      |Relative path <br /> <br />|The relative path indicates the file location on the FTP server where the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] looks for messages. For example, enter **FTPIn** **Caution:** Do not include a backslash (\) in the relative path. You must only provide the folder name where the message is received from. <br />|
      |File mask <br /> <br />|Enter a file mask to identify the message files on the FTP server. <br /> <br />|
      |Transfer mode <br /> <br />|Choose whether messages are transferred from the server using **BINARY** or **ASCII** transfer mode. Always use **BINARY** if the messages are encrypted on the FTP server. <br /> <br />|
      |Use SSL <br /> <br />|Select this check box to use SSL when communicating with the FTP server. <br /> <br />|
      **SFTP**

      |SFTP Receive Setting <br /> <br />|Description <br /> <br />|
      |------------------------|---------------|
      |SFTP server address <br /> <br />|**Required**. The SFTP server address that contains the messages. The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] looks for new messages dropped to a file location this server. <br /> <br />|
      |Port number <br /> <br />|Specifies the port used for communication. The default port is port 22. <br /> <br />|
      |Username <br /> <br />|If the SFTP server requires authentication, enter the username that the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] uses to connect to a location on the SFTP server. <br /> <br />|
      |Password <br /> <br />|Enter the password for the username. <br /> <br />|
      |Confirm password <br /> <br />|Re-enter the username password for the SFTP server. <br /> <br />|
      |Relative path <br /> <br />|The relative path indicates the file location on the SFTP server where the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] looks for messages. For example, enter **FTPIn** **Caution:** Do not include a backslash (\) in the relative path. You must only provide the folder name where the message is received from. <br />|
      |||

   5. Click **Save** to save the route settings.

      > [!NOTE]
      > If more than one route rules are defined, evaluation is based on the first match. The order of executing the rules is defined by the order in which the rules are defined in the grid.

### Message Suspension Settings
Any messages that fail processing can be routed to various endpoints as well. The following table provides the where failed messages can be routed to:

|||
|-|-|
|**Azure BizTalk Bridge** <br /> <br />|Enter the name of the [!INCLUDE[bridge](/Token/bridge_md.md)] to route the message. <br /> <br />The URL looks similar to the following: <br /> <br />https://*YourDeployment*.biztalk.windows.net/default/*BridgeName* <br /> <br />|
|**Azure Blobs** <br /> <br />|Enter the **Shared Access Signature URL** to your [!INCLUDE[azure_2](/Token/azure_2_md.md)] Blob. For example, enter: <br /> <br />https://*myAccount*.blob.core.windows.net/*ContainerName*/*BlobName**PolicyIndentifier**Signature* <br /> <br />[Managing Access to Containers, Blobs, Tables, and Queues](http://go.microsoft.com/fwlink/p/?LinkID=273871) provides more information on the **Shared Access Signature URL**. <br /> <br />|
**Azure [!INCLUDE[sb2](/Token/sb2_md.md)]**

You can route to any of the following [!INCLUDE[sb2](/Token/sb2_md.md)] entities.

|||
|-|-|
|**Queue** <br /> <br />|Provide either the Shared Access Signature (SAS) or the shared secret for the queue. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the queue to route to. </li><li>If you choose the shared secret name, provide the URL for the queue, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>|
|**Topic** <br /> <br />|Provide either the Shared Access Signature (SAS) or the shared secret for the topic. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the topic to route to. </li><li>If you choose the shared secret name, provide the URL for the topic, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>|
|**BasicHttpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
|**WebHttpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
|**NetTcpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
> [!IMPORTANT]
> If you choose to route to a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, make sure the relay endpoint hosts a two-way relay service. You cannot use EDI pipelines to route to a one-way relay service.

Finally, click **Deploy** to deploy the bridge.

## See Also
[Create an EDI bridge using BizTalk Services Portal](/Topic/Create_an_EDI_bridge_using_BizTalk_Services_Portal.md)

