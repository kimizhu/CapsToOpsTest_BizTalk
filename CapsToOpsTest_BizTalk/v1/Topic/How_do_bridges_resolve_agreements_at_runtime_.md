---
description: na
keywords: na
pagetitle: How do bridges resolve agreements at runtime?
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3a8d261-0ada-4798-b079-68ede2cda850
---
# How do bridges resolve agreements at runtime?
How [!INCLUDE[bridge](/Token/bridge_md.md)]s resolve to agreements at runtime.

## How do bridges resolve to agreements?

|Agreement type <br /> <br />|How the resolution happens <br /> <br />|Any user input required? <br /> <br />|
|------------------|------------------------------|----------------------------|
|EDI receive agreement (X12 and EDIFACT) <br /> <br />|The identities (ISA for X12 and UNB for EDIFACT) in the received message are matched with the identities specified in an agreement. If a match happens, that agreement is used for message processing. If the match fails, the message is suspended. <br /> <br />|The EDI message sent to the bridge must include the identities (ISA and UNB). The bridge promotes the identity values, which are used for agreement resolution. <br /> <br />|
|EDI send agreement (X12 and EDIFACT) <br /> <br />|The resolution happens in the following order: <br /> <br /><ol><li>Agreement ID </li><li>Combination of agreement name and partners </li><li>The identities in the agreement </li> </ol>|The EDI message sent to the bridge must include one of the following as part of the header: <br /> <br /><ul><li>“AgreementID” </li><li>“AgreementName”, “HostPartner”, and “GuestPartner” </li><li>“SenderIdentifier”, “SenderQualifier”, “ReceiverIdentifier”, and “ReceiverQualifier” </li> </ul>The bridge promotes these values; which are used for agreement resolution. <br /> <br /><ul><li>If an incorrect agreement ID is included in the message header and subsequently promoted by the bridge, the agreement resolution fails and the message is suspended. </li><li>If agreement and partner names are present in the header, they are promoted by the bridge. If the agreement resolution fails because of incorrect agreement and partner names, the message is suspended. </li><li>If the identities are preset in the header, they are promoted and used for message resolution. </li> </ul>If none of the above values are promoted, agreement resolution fails and the message is suspended. **Note:** For bridges that were deployed before the August update, if none of the properties are present as part of the header, the messages will be processed with the agreement with which they were deployed before the August update. However, if the old bridges are redeployed after the August update, the message sent to the bridges must include the properties in the header, or else the message is suspended. <br />|
|AS2 receive <br /> <br />|The resolution happens based on the AS2-To and AS2-From values specified in the agreement. <br /> <br />|“AS2-To”, “AS2-From”, and “AS2-MessageID” values must be included as per the standard AS2 protocol. The bridge promotes these values, which are then used to match with the values specified in an AS2 agreement. <br /> <br />|
|AS2 send <br /> <br />|The resolution happens based on the AS2-To and AS2-From values specified in the agreement. <br /> <br />|“AS2-To” and “AS2-From” must be included in the message header. <br /> <br />The bridge promotes these values, which are then used to match with the values specified in an AS2 agreement. <br /> <br />|

## What happens to agreements created before the August’ 14 refresh?
As part of the August ’14 refresh of [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], agreement created in [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], and the underlying bridges are decoupled. The following table provides information on how this impacts the existing agreements in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

||Before August’ 14 refresh <br /> <br />|After August’ 14 refresh <br /> <br />|
|-|-----------------------------|----------------------------|
|Agreement <br /> <br />|<ul><li>Agreement exists in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] with a name and an ID. </li><li>Agreements have two bridges underneath; one for send and another for receive, dedicated to the agreement. </li><li>Agreement configuration includes identities, protocol, batch, transform, and transport/route settings. </li> </ul>|<ul><li>Agreement exists in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] with a name and an ID. </li><li>Agreement configuration includes identities, protocol, and batch settings. </li> </ul>|
|Bridge <br /> <br />|<ul><li>Underlying [!INCLUDE[bridge](/Token/bridge_md.md)]s are listed in the **Bridges** tab of the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. </li><li>The [!INCLUDE[bridge](/Token/bridge_md.md)] view is just a listing. You cannot click on a [!INCLUDE[bridge](/Token/bridge_md.md)] to edit its configuration. </li><li>The EDI [!INCLUDE[bridge](/Token/bridge_md.md)]s cannot be deleted from the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. </li> </ul>|<ul><li>The [!INCLUDE[bridge](/Token/bridge_md.md)]s that were earlier associated with an agreement are now listed with their uniquely identifiable URLs. The [!INCLUDE[bridge](/Token/bridge_md.md)]s do not have a name. </li><li>You can click on a bridge to edit its configuration properties. [!INCLUDE[Bridge](/Token/Bridge_md.md)]s are still listed as send and receive side, each denoting a separate [!INCLUDE[bridge](/Token/bridge_md.md)]. </li><li>EDI [!INCLUDE[bridge](/Token/bridge_md.md)]s can be deleted from the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. </li> </ul>|
|Schemas <br /> <br />|Schemas are included as part of agreement configuration. <br /> <br />|Schemas continue to be included as part of agreement configuration. <br /> <br />|
|Transforms <br /> <br />|Transforms are included as part of agreement configuration <br /> <br />|Transform are included as part of [!INCLUDE[bridge](/Token/bridge_md.md)] configuration. <br /> <br />|
|Tracking and archiving <br /> <br />|Tracking and archiving is part of agreement configuration <br /> <br />|Tracking and archiving is part of bridge configuration. <br /> <br />|
|Route acks as flat file <br /> <br />|The configuration option is included as part of agreement configuration <br /> <br />|The configuration option is included as part of bridge configuration. <br /> <br />|

## Community Additions
[Creating EDI Bridges in MABS (post August 2014 Update)](http://tinyurl.com/pjftz5b)

[Using AS2 Bridges in MABS (post August 2014 Update)](http://tinyurl.com/kvghmd3)

## See Also
[EDI, AS2, and EDIFACT Messaging &#40;Business to Business&#41;](/Topic/EDI,_AS2,_and_EDIFACT_Messaging__Business_to_Business).md)

