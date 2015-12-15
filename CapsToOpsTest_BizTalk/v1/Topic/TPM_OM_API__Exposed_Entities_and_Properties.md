---
description: na
keywords: na
pagetitle: TPM OM API: Exposed Entities and Properties
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cbc5d811-89a6-4ef0-b8ea-39f780a8328f
---
# TPM OM API: Exposed Entities and Properties
The TPM OM API reference lists the different entities and their properties that are exposed by the TPM object model.

The `TpmContext` is the base entity and the starting point for all operations related to TPM OM API. The `TpmContext` represents the runtime context of the TPM Data Service. The following entities are part of the TPM Data Service:

## In This Section

|Members <br /> <br />|Description <br /> <br />|
|-----------|---------------|
|[Partner](/Topic/Partner.md) <br /> <br />|Represents all partners within the context. <br /> <br />|
|[BusinessProfile](/Topic/BusinessProfile.md) <br /> <br />|Represents all profiles associated with a partner. <br /> <br />|
|[BusinessIdentity](/Topic/BusinessIdentity.md) <br /> <br />|Represents all identities associated with a profile <br /> <br />|
|[QualifierIdentity](/Topic/QualifierIdentity.md) <br /> <br />|Represents the identifier associated with the Business Identity of a profile. <br /> <br />|
|[Contact&#124; Azure BizTalk Services](/Topic/Contact__Azure_BizTalk_Services.md) <br /> <br />|Represents contact information of a partner or a profile <br /> <br />|
|[CertificateReference](/Topic/CertificateReference.md) <br /> <br />|Represents the reference to certificates in the artifact store <br /> <br />|
|[Partnership](/Topic/Partnership.md) <br /> <br />|Represents a collection of partnerships <br /> <br />|
|[Agreement](/Topic/Agreement.md) <br /> <br />|Represents a collection of all agreements <br /> <br />|
|[ProtocolSettings](/Topic/ProtocolSettings.md) <br /> <br />|Represents the abstract protocol settings for an agreement <br /> <br />|
|[X12ProtocolSettings](/Topic/X12ProtocolSettings.md) <br /> <br />|Represents the X12 protocol settings for an agreement <br /> <br />|
|[EDIFACTProtocolSettings](/Topic/EDIFACTProtocolSettings.md) <br /> <br />|Represents the EDIFACT protocol settings for an agreement <br /> <br />|
|[AS2ProtocolSettings](/Topic/AS2ProtocolSettings.md) <br /> <br />|Represents the AS2 protocol settings for an agreement <br /> <br />|
|[BatchDescription](/Topic/BatchDescription.md) <br /> <br />|Represents a collection of batch descriptions <br /> <br />|
|[OnewayAgreement](/Topic/OnewayAgreement.md) <br /> <br />|Represents a collection of one-way agreements <br /> <br />|
|[X12EnvelopeOverride](/Topic/X12EnvelopeOverride.md) <br /> <br />|Represents the envelope definitions for a message type <br /> <br />|
|[X12DelimiterOverrides](/Topic/X12DelimiterOverrides.md) <br /> <br />|Represents the delimiter definitions for a message type <br /> <br />|
|[X12SchemaReference](/Topic/X12SchemaReference.md) <br /> <br />|Represents the schema reference for a message type <br /> <br />|
|[X12ValidationOverride](/Topic/X12ValidationOverride.md) <br /> <br />|Represents the validation settings for a message type <br /> <br />|
|[EDIFACTEnvelopeOverrides](/Topic/EDIFACTEnvelopeOverrides.md) <br /> <br />|Represents the envelope definitions for a message type <br /> <br />|
|[EDIFACTDelimiterOverride](/Topic/EDIFACTDelimiterOverride.md) <br /> <br />|Represents the delimiter definitions for a message type <br /> <br />|
|[EDIFACTSchemaReference](/Topic/EDIFACTSchemaReference.md) <br /> <br />|Represents the schema reference for a message type <br /> <br />|
|[EDIFACTValidationOverrides](/Topic/EDIFACTValidationOverrides.md) <br /> <br />|Represents the validation settings for a message type <br /> <br />|
|[CustomSetting](/Topic/CustomSetting.md) <br /> <br />|Represents the custom settings for different entities: <br /> <br /><ul><li>For a profile, this stores the templates. </li> </ul>|
