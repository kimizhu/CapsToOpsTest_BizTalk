---
description: na
keywords: na
pagetitle: Configure EDI Receive bridge settings in BizTalk Services Portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 256222ee-5a82-442c-8ab3-d6434c2cc479
---
# Configure EDI Receive bridge settings in BizTalk Services Portal
Configure an EDI receive bridge in [!INCLUDE[af_integration](/Token/af_integration_md.md)]. The EDI receive bridge configuration includes settings including which transport to use for receiving messages, any transforms to use while processing the message, and routing rules/destinations.

## Configure the Transport
In the **Transport** page, you enter the transport settings used between the two partners. The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] supports HTTP, FTP, SFTP, and AS2 transports. From the **Receive Settings** tab, you can also promote properties from the SOAP and HTTP headers on the received message that can later be used during the agreement processing. You can also use these properties for routing messages to their destinations.

The **Receive Settings** tab is available only after the **General Settings** for a bridge are entered.

#### HTTP transport settings

1. On the **Transport** page, choose **Http** in the **Transport Type** drop down box.

2. The **Endpoint** URL is automatically populated with the address that is used to input messages to the Receive pipeline.

   You can keep the default GUID included in the URL or replace the GUID with another value of your choice. The value you provide must be unique. This URL represents the endpoint at which the hosted partner receives a message from the guest partner.

#### FTP transport settings

1. On the **Transport** page, choose **FTP** in the **Transport Type** drop down box.

2. Enter your FTP server receive settings:

   |FTP Receive Setting <br /> <br />|Description <br /> <br />|
   |-----------------------|---------------|
   |FTP server address <br /> <br />|**Required**. Enter the FTP server address that contains the messages. The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] looks for new messages dropped to a file location this server. <br /> <br />|
   |Port number <br /> <br />|Enter the TCP port the FTP server is configured to use. The default port is port 21. <br /> <br />|
   |Username <br /> <br />|If the FTP server requires authentication, enter the username that the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] uses to connect to a file location on the FTP server. <br /> <br />|
   |Password <br /> <br />|Enter the password for the username. <br /> <br />|
   |Confirm password <br /> <br />|Re-enter the username password for the FTP server. <br /> <br />|
   |Relative path <br /> <br />|The relative path indicates the file location on the FTP server where the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] looks for messages. For example, enter **FTPIn**. **Caution:** Do not include a backslash (\) in the relative path. You must only provide the folder name where the message is received from. <br />|
   |File mask <br /> <br />|Enter a file mask to identify the message files on the FTP server. <br /> <br />|
   |Transfer mode <br /> <br />|Choose whether messages are transferred from the server using **BINARY** or **ASCII** transfer mode. Always use **BINARY** if the messages are encrypted on the FTP server. <br /> <br />|
   |Use SSL <br /> <br />|Uses SSL when communicating with the FTP server. <br /> <br />|

#### SFTP transport settings

1. On the **Transport** page, choose **SFTP** in the **Transport Type** drop down box.

2. Enter your SFTP server receive settings:

   |SFTP Receive Setting <br /> <br />|Description <br /> <br />|
   |------------------------|---------------|
   |SFTP server address <br /> <br />|**Required**. Enter the SFTP server address that contains the messages. The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] looks for new messages dropped to a file location this server. <br /> <br />|
   |Port number <br /> <br />|Enter the TCP port used for communication. The default port is port 22. <br /> <br />|
   |Username <br /> <br />|If the SFTP server requires authentication, enter the username that the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] uses to connect to a location on the SFTP server. <br /> <br />|
   |Password <br /> <br />|Enter the password for the username. <br /> <br />|
   |Confirm password <br /> <br />|Re-enter the username password for the SFTP server. <br /> <br />|
   |Relative path <br /> <br />|The relative path indicates the file location on the SFTP server where the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] looks for messages. For example, enter **FTPIn**. **Caution:** Do not include a backslash (\) in the relative path. You must only provide the folder name where the message is received from. <br />|
   |File mask <br /> <br />|Enter a file mask to identify the message files on the SFTP server. <br /> <br />|

#### AS2 transport settings

1. To configure an AS2 transport, you must have already configured an AS2 agreement. See [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md) to create an AS2 agreement.

2. On the **Transport** page, choose **AS2** in the **Transport Type** drop down box.

3. Select your AS2 agreement.

#### Promote SOAP and HTTP properties

1. On the **Transport** page, expand the **Promoted Properties** section, and then select the (**+**) sign to promote a property. The following table details the fields and the values you must enter:

   |Field <br /> <br />|Description <br /> <br />|
   |---------|---------------|
   |Source Type <br /> <br />|Select the message type from which the header values are extracted. For assigning header values to properties, the possible values are **SOAP** and **HTTP**. <br /> <br />|
   |Property Name <br /> <br />|Enter the name of the property that you are defining. For example, you can set this to **MsgType**. <br /> <br />|
   |Identifier <br /> <br />|Enter the name of property present in the message header, the value of which you want to extract and assign to a property that you are defining. You can also promote the value of custom header properties. For example, in the following excerpt, **MessageType** is a custom header. <br /> <br />DELETED CODE <br /> <br />So, if you set the Identifier property **MessageType**, then the value of the header from the incoming message is extracted and is assigned to the **MsgType** property that you are defining as part of the agreement. <br /> <br />|
   |Namespace <br /> <br />|Specify the SOAP header namespace. Going by the excerpt used above, the namespace for the **MessageType** custom header is highlighted. <br /> <br />DELETED CODE <br /> <br />You do not need to provide a namespace if you are promoting a property from an HTTP message header. <br /> <br />|

## Configure the Transform
On the **[!INCLUDE[transform](/Token/transform_md.md)]** page, you can:

- Upload an existing [!INCLUDE[transform](/Token/transform_md.md)] to map the incoming message to another message structure. See [Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md) to create a [!INCLUDE[transform](/Token/transform_md.md)],.

- If the [!INCLUDE[transform](/Token/transform_md.md)] uses a C# Scripting [!INCLUDE[mapop](/Token/mapop_md.md)], you can also upload the required assemblies as part of the agreement.

- On the **[!INCLUDE[transform](/Token/transform_md.md)]** page, you can promote properties on the incoming message based on XPath and Lookup queries.

### Add a Transform
Go to the **[!INCLUDE[transform](/Token/transform_md.md)]s** page. If [!INCLUDE[transform](/Token/transform_md.md)]s are already uploaded, you can select the [!INCLUDE[transform](/Token/transform_md.md)] from the drop-down. If [!INCLUDE[transform](/Token/transform_md.md)]s have not been uploaded:

1. Select **Upload** and browse for the [!INCLUDE[transform](/Token/transform_md.md)].

2. In the dialog window, select the [!INCLUDE[transform](/Token/transform_md.md)] file (*FileName*.trfm), and select **Open**.

3. The selected [!INCLUDE[transform](/Token/transform_md.md)] is added to the list of [!INCLUDE[transform](/Token/transform_md.md)]s.

### Add an assembly
If the [!INCLUDE[transform](/Token/transform_md.md)] you are using includes an external file assembly (.dll), then you must also upload the assembly:

1. Expand the **Assembly** section.

2. Select **Upload** to browse to the .dll assembly.

### Promote a Property
On the **[!INCLUDE[transform](/Token/transform_md.md)]s** page, expand the **Promoted Properties** section. The following options are available:

#### <a name="BKMK_RecXPath"></a>Promote a property using XPath queries

1. Under the **XPath** section, for **Property Name**, enter the name of the property you are defining. The value of this property is set to the value that is extracted from the message body using the XPath query.

2. In **Schema**, select the schema for the incoming message. If the schema is not listed, upload it by selecting **Upload**.

3. In **XPath**, enter the XPath query to extract an element or an attribute from a message. A typical XPath query looks like the following:

   ' /&#42;[local-name()='*&lt;root_node&gt;*' and namespace-uri()='*&lt;namespace&gt;*']/&#42;[local-name()='*&lt;node_name&gt;*' and namespace-uri()=*&lt;namespace&gt;*']/&#42;@[local-name()='*&lt;attribute_name&gt;*' and namespace-uri()='*&lt;namespace&gt;*'] &#96;

   > [!TIP]
   > You can get an XPath query from the schema editor. In the Schema Editor available as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], select the schema element for which you want the XPath query. In the Properties window, look for the value of the **Instance Xpath** property. That should be the XPath query for the node.

#### <a name="BKMK_RecLookup"></a>Promote a property using lookup

1. Under the **Lookup** section, for **Property Name**, enter the name of the property you are defining. The value of this property is set to the value extracted using the lookup configuration you are defining.

2. In **Connection URL**, enter a valid connection URL to connect to a [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)].

3. In **Table Name**, enter the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] table name to query.

4. In **Query Out Column**, enter a column name in the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] table. This value is used as the output value that gets assigned to the looked up property.

5. In **Query In Column**, enter a column name in the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] table. This value is used as the input query for performing the data lookup.

6. In **Input Property**, select a property. The value of this property is passed to the **Query In Column**.

To understand how Lookup is used at run-time, assume a **TempTable** table exists in a [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] database. This table has two columns: **PurchaseOrder** and **CustomerName**. Let’s assume that you previously promoted a property called **P1** as part of the agreement.

|||
|-|-|
|PropertyName <br /> <br />|**P2**. This is the property that contains the value promoted using a Lookup. <br /> <br />|
|TableName <br /> <br />|**TempTable** <br /> <br />|
|Query In Column <br /> <br />|**PurchaseOrder** <br /> <br />|
|Query Out Column <br /> <br />|**CustomerName** <br /> <br />|
|Input Query <br /> <br />|**P1**. You could have promoted this property earlier either using XPath or from the SOAP or HTTP message header. Assume the value of P1, at runtime, is set to **PO1234**. <br /> <br />|
This is how the configuration is used:

- The agreement looks up the value of P1 (**PO1234**) in the input query column (**PurchaseOrder**) in the table (**TempTable**).

- The agreement then picks up the value corresponding to **PO1234** from the output query column (**CustomerName**) in the **TempTable**.

- The value picked up from the output query column is assigned to the property P2. For example, if the customer name corresponding to purchase order **PO1234** is **John**, then the value of P2 is set to John.

## Configure the Route
Use the **Route** page to:

- Set route conditions/rules based on which messages are routed to destination endpoints.

- Set route actions. Route actions can be used to include specific message headers (for SOAP and HTTP) before the message is sent to the destination endpoint.

- Set route destinations for messages that are successfully processed or get suspended.

- Set message suspensions settings for routing a suspended message to a [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)], [!INCLUDE[Azure_2](/Token/Azure_2_md.md)] Blobs, or [!INCLUDE[Azure_2](/Token/Azure_2_md.md)][!INCLUDE[sb2](/Token/sb2_md.md)].

### Route Settings

1. On the **Route** page, expand **Route Settings**, select the **Route acks as flat file** checkbox to receive a flat-file acknowledgement from the trading partner. Click **Add**.

2. In the **New Route Rule** dialog box, you specify three key routing configurations – routing condition, routing action, and routing destination.

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
      |**Azure Blobs** <br /> <br />|Enter the **Shared Access Signature URL** to your [!INCLUDE[Azure_2](/Token/Azure_2_md.md)] Blob. For example, enter: <br /> <br />https://*myAccount*.blob.core.windows.net/*ContainerName*/*BlobName**PolicyIndentifier**Signature* <br /> <br />[Managing Access to Containers, Blobs, Tables, and Queues](http://go.microsoft.com/fwlink/p/?LinkID=273871) provides more information on the **Shared Access Signature URL**. <br /> <br />|
      |**Azure [!INCLUDE[sb2](/Token/sb2_md.md)]** <br /> <br />|You can route to any of the following [!INCLUDE[sb2](/Token/sb2_md.md)] entities. <br /> <br />**Queue** <br /> <br />Provide either the Shared Access Signature (SAS) or the shared secret for the queue. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the queue to route to. </li><li>If you choose the shared secret name, provide the URL for the queue, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>**Topic** <br /> <br />Provide either the Shared Access Signature (SAS) or the shared secret for the topic. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the topic to route to. </li><li>If you choose the shared secret name, provide the URL for the topic, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>**BasicHttpRelay** <br /> <br />Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />**WebHttpRelay** <br /> <br />Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />**NetTcpRelay** <br /> <br />Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. **Important:** If you choose to route to a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, make sure the relay endpoint hosts a two-way relay service. You cannot use EDI pipelines to route to a one-way relay service. <br />|

   5. Click **Save** to save the route settings.

      > [!NOTE]
      > If more than one route rules are defined, evaluation is based on the first match. The order of executing the rules is defined by the order in which the rules are defined in the grid.

### Message Suspension Settings
Any messages that fail processing can be routed to various endpoints as well. The following table provides the where failed messages can be routed to:

|||
|-|-|
|**Azure BizTalk Bridge** <br /> <br />|Enter the name of the [!INCLUDE[bridge](/Token/bridge_md.md)] to route the message. <br /> <br />The URL looks similar to the following: <br /> <br />https://*YourDeployment*.biztalk.windows.net/default/*BridgeName* <br /> <br />|
|**Azure Blobs** <br /> <br />|Enter the **Shared Access Signature URL** to your [!INCLUDE[Azure_2](/Token/Azure_2_md.md)] Blob. For example, enter: <br /> <br />https://*myAccount*.blob.core.windows.net/*ContainerName*/*BlobName**PolicyIndentifier**Signature* <br /> <br />[Managing Access to Containers, Blobs, Tables, and Queues](http://go.microsoft.com/fwlink/p/?LinkID=273871) provides more information on the **Shared Access Signature URL**. <br /> <br />|
|**Azure [!INCLUDE[sb2](/Token/sb2_md.md)]** <br /> <br />|You can route to any of the following [!INCLUDE[sb2](/Token/sb2_md.md)] entities. <br /> <br />**Queue** <br /> <br />Provide either the Shared Access Signature (SAS) or the shared secret for the queue. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the queue to route to. </li><li>If you choose the shared secret name, provide the URL for the queue, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>**Topic** <br /> <br />Provide either the Shared Access Signature (SAS) or the shared secret for the topic. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the topic to route to. </li><li>If you choose the shared secret name, provide the URL for the topic, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>**BasicHttpRelay** <br /> <br />Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />**WebHttpRelay** <br /> <br />Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />**NetTcpRelay** <br /> <br />Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. **Important:** If you choose to route to a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, make sure the relay endpoint hosts a two-way relay service. You cannot use EDI pipelines to route to a one-way relay service. <br />|

## See Also
[Create an EDI bridge using BizTalk Services Portal](/Topic/Create_an_EDI_bridge_using_BizTalk_Services_Portal.md)

