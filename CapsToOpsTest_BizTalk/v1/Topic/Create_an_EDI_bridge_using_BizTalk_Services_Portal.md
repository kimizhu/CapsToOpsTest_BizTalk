---
description: na
keywords: na
pagetitle: Create an EDI bridge using BizTalk Services Portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 458c2c17-be30-4fdb-b438-5683e38dd9c9
---
# Create an EDI bridge using BizTalk Services Portal
How to create an EDI [!INCLUDE[bridge](/Token/bridge_md.md)] in [!INCLUDE[af_integration](/Token/af_integration_md.md)]. EDI bridges are used to process X12 and EDIFACT messages.

You can create [!INCLUDE[bridge](/Token/bridge_md.md)]s to process EDI messages directly from the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. Bridge configuration includes information such as which messaging transport to use, transforms (if required), and where the messages are routed. The [!INCLUDE[bridge](/Token/bridge_md.md)]s associate with the EDI agreements at runtime and use the EDI protocol-related settings that are defined as part of the agreement. See [How do bridges resolve agreements at runtime?](/Topic/How_do_bridges_resolve_agreements_at_runtime_.md)

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], click the **Bridges** tab, and then click **Add**.

2. In the General Settings tab, for **Protocol**, select **EDI**.

3. Under **Tracking**, enter how you want to track the messages:

   |||
   |-|-|
   |Track Send side message properties <br /> <br />|Check this to store the message properties when the EDI message is sent to the partner. Once stored, you can query this data by clicking Tracking on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page. <br /> <br />When enabled, you can also store the message body by checking **Archive Send side message** (Developer and Premium Editions only). <br /> <br />|
   |Track Receive side message properties <br /> <br />|Check this to store the message properties when the EDI message is received from a partner. Once stored, you can query this data by clicking Tracking on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page. <br /> <br />When enabled, you can also store the message body by checking **Archive Receive side message** (Developer and Premium Editions only). <br /> <br />|

4. Expand **EDIFACT Delimiters** and provide the relevant values. These values are used to parse the incoming EDIFACT message to retrieve partner identities, etc. Why do we only need EDIFACT delimiters and not X12? That’s because the ISA segment is mandatory in an X12 message and the bridge can extract the required delimiters from the ISA segment. For EDIFACT, a UNA segment is optional. So, the bridge needs to be aware of the delimiters to use for parsing the message, in case the incoming EDIFACT message does not have the UNA segment. If the incoming EDIFACT message includes a UNA segment, the values you provide here will be ignored.

   |||
   |-|-|
   |UNA1 (Component data element separator) <br /> <br />|Enter a value for the component data element separator that separates simple data elements within composite data elements. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |UNA2 (Data element separator) <br /> <br />|Enter a value for the data element separator that separates composite data elements consisting of two or more simple data elements or simple data elements that are not part of a composite. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |UNA3 (Decimal notation) <br /> <br />|Specify whether you want to use a **Comma** or **Decimal** as the decimal notation to be used in the outgoing interchange. <br /> <br />|
   |UNA4 (Release Indicator) <br /> <br />|Enter a value for the release indicator that indicates that the following character is not a syntax separator, terminator, or release character, but is part of the original data. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |UNA5 (Repetition Separator) <br /> <br />|Enter a value for the repetition separator that is used to separate segments that repeat within a transaction set. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |UNA6 (Segment Terminator) <br /> <br />|Enter a value for the segment terminator that indicates the end of an EDI segment. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
   |Suffix <br /> <br />|Specify whether you want to use carriage return (CR), line feed (LF), both, or none as the end-of-line character that is used with the segment terminator. <br /> <br />|

5. Click **Continue**. **Receive Settings** and **Send Settings** tabs are added. See [Configure EDI Receive bridge settings in BizTalk Services Portal](/Topic/Configure_EDI_Receive_bridge_settings_in_BizTalk_Services_Portal.md) and [Configure EDI Send bridge settings in BizTalk Services Portal](/Topic/Configure_EDI_Send_bridge_settings_in_BizTalk_Services_Portal.md) to configure the receive and send settings.

## Next

- [Configure EDI Receive bridge settings in BizTalk Services Portal](/Topic/Configure_EDI_Receive_bridge_settings_in_BizTalk_Services_Portal.md)

- [Configure EDI Send bridge settings in BizTalk Services Portal](/Topic/Configure_EDI_Send_bridge_settings_in_BizTalk_Services_Portal.md)

