---
description: na
keywords: na
pagetitle: Create an AS2 bridge using BizTalk Services Portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7894ebb3-c8f9-45db-942b-ed487656d6b9
---
# Create an AS2 bridge using BizTalk Services Portal
This topic shows how to create an AS2 [!INCLUDE[bridge](/Token/bridge_md.md)] in [!INCLUDE[azure_2](/Token/azure_2_md.md)][!INCLUDE[af_integration](/Token/af_integration_md.md)]. AS2 bridges are used to transfer messages over an AS2 protocol.

You can create [!INCLUDE[bridge](/Token/bridge_md.md)]s to process AS2 messages directly from the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. Bridge configuration includes information such as which messaging transport to use, transforms (if required), and where the messages must be routed to. [!INCLUDE[bridge](/Token/bridge_md.md)]s are associated with the AS2 agreements at runtime and use the AS2 protocol-related settings that are defined as part of the agreement. See [How do bridges resolve agreements at runtime?](/Topic/How_do_bridges_resolve_agreements_at_runtime_.md).

In this topic:

[Create an AS2 bridge](/Topic/Create_an_AS2_bridge_using_BizTalk_Services_Portal.md#BKMK_CreateAS2bridge)

[Configure the AS2 Receive bridge settings](/Topic/Create_an_AS2_bridge_using_BizTalk_Services_Portal.md#BKMK_AS2bridgeReceive)

[Configure the AS2 Send bridge settings](/Topic/Create_an_AS2_bridge_using_BizTalk_Services_Portal.md#BKMK_AS2bridgeSend)

## <a name="BKMK_CreateAS2bridge"></a>Create an AS2 bridge

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], click the **Bridges** tab, and then click **Add**.

2. In the General Settings tab for **Protocol**, select **AS2**.

3. Under **Tracking**, enter how you want to track the messages:

   |||
   |-|-|
   |Track Send side message properties <br /> <br />|Check this to store the message properties when the AS2 message is sent to the partner. Once stored, you can query this data by clicking **Tracking** on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page. <br /> <br />When enabled, you can also store the message body by checking **Track Send side message body**. <br /> <br />|
   |Archive Send side encoded message <br /> <br />|When **Track Send side message properties** is enabled, stores encoded AS2 messages sent to a partner. <br /> <br />For example, when an AS2 message is encrypted, decoding the message decrypts the message. The decrypted output is stored. <br /> <br />For example, when an AS2 message is not encrypted, encoding the message encrypts the message. The encrypted message body is stored. **Note:** Applies to Developer and Premium Editions only. <br />|
   |Archive Send side decoded message <br /> <br />|When **Track Send side message properties** is enabled, stores decoded AS2 messages sent to a partner. <br /> <br />For example, when an AS2 message is encrypted, decoding the message decrypts the message. The decrypted message body is stored. **Note:** Applies to Developer and Premium Editions only. <br />|
   |Track Receive side message properties <br /> <br />|Check this to store the message properties when the AS2 message is received from a partner. Once stored, you can query this data by clicking Tracking on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page. <br /> <br />When enabled, you can also store the message body by checking **Track Receive side message body**. <br /> <br />|
   |Archive Receive side encoded message <br /> <br />|When **Track Recive side message properties** is enabled, stores encoded AS2 messages received from a partner. <br /> <br />For example, when an AS2 message is not encrypted, encoding the message encrypts the message. The encrypted message body is stored. **Note:** Applies to Developer and Premium Editions only. <br />|
   |Archive Receive side decoded message <br /> <br />|When **Track Recive side message properties** is enabled, stores decoded AS2 messages received from a partner. <br /> <br />For example, when an AS2 message is encrypted, decoding the message decrypts the message. The decrypted message body is stored. **Note:** Applies to Developer and Premium Editions only. <br />|

4. Expand **EDIFACT Delimiters** and provide the relevant values. These values are used to parse the incoming EDIFACT message to retrieve partner identities, etc. Why do we only need EDIFACT delimiters and not X12? That’s because the ISA segment is mandatory in an X12 message and the bridge can extract the required delimiters from the ISA segment. For EDIFACT, a UNA segment is optional. So, the bridge needs to be aware of the delimiters to use for parsing the message, in case the incoming EDIFACT message does not have the UNA segment. If the incoming EDIFACT message includes a UNA segment, the values you enter here are ignored.

   |||
   |-|-|
   |UNA1 (Component data element separator) <br /> <br />|Enter a value for the component data element separator that separates simple data elements within composite data elements. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |UNA2 (Data element separator) <br /> <br />|Enter a value for the data element separator that separates composite data elements consisting of two or more simple data elements or simple data elements that are not part of a composite. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |UNA3 (Decimal notation) <br /> <br />|Specify whether you want to use a **Comma** or **Decimal** as the decimal notation to be used in the outgoing interchange. <br /> <br />|
   |UNA4 (Release Indicator) <br /> <br />|Enter a value for the release indicator that indicates that the following character is not a syntax separator, terminator, or release character, but is part of the original data. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |UNA5 (Repetition Separator) <br /> <br />|Enter a value for the repetition separator that is used to separate segments that repeat within a transaction set. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |UNA6 (Segment Terminator) <br /> <br />|Enter a value for the segment terminator that indicates the end of an EDI segment. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |Suffix <br /> <br />|Specify whether you want to use carriage return (CR), line feed (LF), both, or none as the end-of-line character that is used with the segment terminator. <br /> <br />|

5. Click **Continue**. **Receive Settings** and **Send Settings** tabs are added.

## <a name="BKMK_AS2bridgeReceive"></a>Configure the AS2 Receive bridge settings
In the receive settings, you enter the inbound URL and the route settings to receive messages over AS2.

### Inbound URL settings
These settings define the endpoint where the hosted partner in an agreement receives incoming AS2 messages.

On the **Inbound URL** page of the **Receive Settings** tab, enter the following values:

|||
|-|-|
|**URL Suffix** <br /> <br />|Enter a unique URL suffix to append to the URL. The guest partner sends AS2 messages to the URL, which includes this suffix. <br /> <br />|
|**URL** <br /> <br />|This read-only field shows the endpoint URL at which the hosted partner receives incoming AS2 messages. The complete URL includes the URL suffix you provided. <br /> <br />|

### Route settings
AS2 messages can be sent to a non-EDI destination or received from a non-EDI destination. An AS2 message can be routed to [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)]s, [!INCLUDE[azure_2](/Token/azure_2_md.md)] blobs, or [!INCLUDE[azure_2](/Token/azure_2_md.md)][!INCLUDE[sb2](/Token/sb2_md.md)]. This section provides information on how to create routing rules to route to these destinations.

1. On the **Route** page of the **Receive Settings** tab, expand **Route Settings**, and then click **Add**.

2. In the dialog box that pops us, you specify three key routing configurations – routing condition, routing action, and routing destination.

   1. Enter a unique name for the routing rule.

   2. **Route Rule**: Enter the routing condition based on the properties you promoted earlier. You can either use the grid to specify the condition or provide a SQL 92 filter expression that specifies the condition. To understand this better, let us assume you promoted a property (**CustName**) whose value is set to **John** at runtime. To use this property as a routing condition, you can do either of the following:

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

   4. **Route destination**: Enter the destination where the messages are routed once they are processed by the agreement:

      > [!NOTE]
      > Even if you do not enter a routing condition and a routing action, you must enter a routing destination.

      |||
      |-|-|
      |**Azure BizTalk Bridge** <br /> <br />|Enter the name of the [!INCLUDE[bridge](/Token/bridge_md.md)] to route the message. <br /> <br />The URL looks similar to the following: <br /> <br />https://*YourDeployment*.biztalk.windows.net/default/*BridgeName* <br /> <br />|
      |**Azure Blobs** <br /> <br />|Enter the **Shared Access Signature URL** to your [!INCLUDE[azure_2](/Token/azure_2_md.md)] Blob. For example, enter: <br /> <br />https://*myAccount*.blob.core.windows.net/*ContainerName*/*BlobName**PolicyIndentifier**Signature* <br /> <br />[Managing Access to Containers, Blobs, Tables, and Queues](http://go.microsoft.com/fwlink/p/?LinkID=273871) provides more information on the **Shared Access Signature URL**. <br /> <br />|
      **Azure [!INCLUDE[sb2](/Token/sb2_md.md)]**

      You can route to any of the following [!INCLUDE[sb2](/Token/sb2_md.md)] entities:

      |||
      |-|-|
      |**Queue** <br /> <br />|Provide either the Shared Access Signature (SAS) or the shared secret for the queue. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the queue to route to. </li><li>If you choose the shared secret name, provide the URL for the queue, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>|
      |**Topic** <br /> <br />|Provide either the Shared Access Signature (SAS) or the shared secret for the topic. <br /> <br /><ul><li>If you choose the SAS option, provide the SAS connection string and the name of the topic to route to. </li><li>If you choose the shared secret name, provide the URL for the topic, [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. </li> </ul>|
      |**BasicHttpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
      |**WebHttpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
      |**NetTcpRelay** <br /> <br />|Provide the URL for the relay endpoint, the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name, and the [!INCLUDE[sb2](/Token/sb2_md.md)] issuer key. <br /> <br />|
      > [!IMPORTANT]
      > If you choose to route to a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, make sure the relay endpoint hosts a two-way relay service. You cannot use EDI pipelines to route to a one-way relay service.

   5. Click **Save** to save the route settings.

      > [!NOTE]
      > If more than one route rules are defined, evaluation is based on the first match. The order of executing the rules is defined by the order in which the rules are defined in the grid.

## <a name="BKMK_AS2bridgeSend"></a>Configure the AS2 Send bridge settings
In the send settings, you enter the inbound URL and the route settings to send messages over AS2. You send a message to the inbound URL to be routed to the guest partner’s destination URL.

### Inbound URL settings
These settings define the endpoint where the hosted partner receives AS2 messages to be sent to the guest partner.

On the **Inbound URL** page of the **Send Settings** tab, enter the following values:

|||
|-|-|
|**URL Suffix** <br /> <br />|Enter a unique URL suffix to append to the URL. The hosted partner receives AS2 messages at this endpoint URL, which includes this suffix. <br /> <br />|
|**URL** <br /> <br />|This read-only field shows the endpoint URL at which the hosted partner receives AS2 messages to be sent to a guest partner. The complete URL includes the URL suffix you provided. <br /> <br />|

### Transport settings
AS2 messages can be routed to a destination URL endpoint. Basically, you configure the transport settings for the endpoint where the message must be routed to.

On the **Transport** page of the **Send Settings** tab, enter a destination URL. This URL is used to send AS2 messages from the hosted partner to the guest partner.

## See Also
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

