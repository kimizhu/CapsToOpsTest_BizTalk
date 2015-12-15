---
description: na
keywords: na
pagetitle: EDIFACTEnvelopeOverrides
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6228c140-1695-4bb9-a5e8-e4f43d858876
---
# EDIFACTEnvelopeOverrides
The `EDIFACTEnvelopeOverride` entity captures the EDIFACT envelope override settings associated with an EDIFACT protocol setting.

## <a name="BKMK_CreateEntity"></a>EDIFACTEnvelopeOverrides Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|A unique ID for the EDIFACT envelope overrides settings. This value is auto-generated. <br /> <br />|
|ApplicationPassword <br /> <br />|String <br /> <br />|The UNG8 application password. <br /> <br />|
|AssociationAssignedCode <br /> <br />|String <br /> <br />|This is derived from the schema. <br /> <br />|
|ControllingAgencyCode <br /> <br />|String <br /> <br />|The UNG6 controlling agency code. <br /> <br />|
|FunctionalGroupId <br /> <br />|String <br /> <br />|**Required**. The UNG1 functional group ID. <br /> <br />|
|GroupHeaderMessageVersion <br /> <br />|String <br /> <br />|The group header message version (UNG7.1). <br /> <br />|
|GroupHeaderMessageRelease <br /> <br />|String <br /> <br />|The group header message release (UNG7.2). <br /> <br />|
|MessageAssociationAssignedCode <br /> <br />|String <br /> <br />|The message association assigned code (UNG7.3). <br /> <br />|
|MessageId <br /> <br />|String <br /> <br />|**Required**. This is derived from the schema. <br /> <br />|
|MessageVersion <br /> <br />|String <br /> <br />|**Required**. This is derived from the schema. <br /> <br />|
|MessageRelease <br /> <br />|Short <br /> <br />|**Required**. This is derived from the schema. <br /> <br />|
|ReceiverApplicationId <br /> <br />|String <br /> <br />|The receiver application ID (UNG3.1). <br /> <br />|
|ReccceiverApplicationQualifier <br /> <br />|String <br /> <br />|The receiver application qualifier (UNG3.2). <br /> <br />|
|SenderApplicationId <br /> <br />|String <br /> <br />|The sender application ID (UNG2.1). <br /> <br />|
|SenderApplicationQualifier <br /> <br />|String <br /> <br />|The sender application qualifier (UNG2.2). <br /> <br />|
|EDIFACTProtocolSettings <br /> <br />|EDIFACTProtocolSettings <br /> <br />|**Required**. A navigation property that references the EDIFACT protocol settings associated with the overrides. <br /> <br />|
|EDIFACTProtocolSettingsId <br /> <br />|Int <br /> <br />|**Required**. The EDIFACT protocol settings ID. <br /> <br />|
|TargetNamespace <br /> <br />|String <br /> <br />|The target namespace string, for example: **http://schemas.microsoft.com/BizTalk/EDI/EDIFACT/2006#EFACT_D98A_APERAK**. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

