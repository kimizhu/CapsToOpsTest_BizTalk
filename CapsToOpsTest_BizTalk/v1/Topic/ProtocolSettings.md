---
description: na
keywords: na
pagetitle: ProtocolSettings
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39c9beb5-e154-447e-ba22-f173d939b104
---
# ProtocolSettings
A `ProtocolSettings` entity is an abstract entity that defines the protocol settings common to X12 and AS2 protocols. The `X12ProtocolSettings` and `AS2ProtocolSettings` entities derive from the `ProtocolSettings` entity. The `ProtocolSettings` entity cannot be instantiated. You must instead instantiate [X12ProtocolSettings](/Topic/X12ProtocolSettings.md) or [AS2ProtocolSettings](/Topic/AS2ProtocolSettings.md).

- [ProtocolSettings Entity Properties](/Topic/ProtocolSettings.md#BKMK_ProtocolSettingsProps)

## <a name="BKMK_ProtocolSettingsProps"></a>ProtocolSettings Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the protocol settings. This value is auto-generated. <br /> <br />|
|Name <br /> <br />|String <br /> <br />|**Required**. Specifies a unique name for the protocol settings. This must not be more than 256 characters. <br /> <br />|
|ProtocolName <br /> <br />|String <br /> <br />|**Required**. Set this to **X12** for an X12 agreement or **AS2** for an AS2 agreement. This value must not be more than 50 characters and is case-insensitive. <br /> <br />|
|BusinessProfile <br /> <br />|BusinessProfile <br /> <br />|A navigation property that references the business profile to which the protocol settings belong. <br /> <br />|
|OnewayAgreement <br /> <br />|OnewayAgreement <br /> <br />|A navigation property that references the agreement with which the protocol settings is associated. <br /> <br />|

## Considerations
A `ProtocolSettings` entity must be associated with a `BusinessProfile`, `AgreementAsSender`, or `AgreementAsReceiver`.

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

