---
description: na
keywords: na
pagetitle: EDIFACTValidationOverrides
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e19ca99f-3d01-4cab-a670-7e922ecc713a
---
# EDIFACTValidationOverrides
The `EDIFACTValidationOverrides` entity captures the EDIFACT validation override settings associated with an EDIFACT protocol setting.

## <a name="BKMK_EntityProps"></a>EDIFACTValidationOverrides Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the EDIFACT validation override. This value is auto-generated. <br /> <br />|
|AllowLeadingAndTrailingSpacesAndZeroes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether leading and trailing spaces must be allowed. <br /> <br />|
|EnforceCharacterSet <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether character set validation is enforced using the override. <br /> <br />|
|MessageId <br /> <br />|String <br /> <br />|**Required**. Specifies the message ID. This value must not be a duplicate in the context of the same EDIFACTProtocolSettings. <br /> <br />|
|EDIFACTProtocolSettings <br /> <br />|EDIFACTProtocolSettings <br /> <br />|**Required**. A navigation property that references the EDIFACT protocol settings associated with the overrides. <br /> <br />|
|EDIFACTProtocolSettingsId <br /> <br />|Int <br /> <br />|**Required**. A navigation property that references an EDIFACT protocol settings ID. <br /> <br />|
|SeparatorPolicy <br /> <br />|Short <br /> <br />|**Required**. Specifies the separator policy. The possible values are 0 (for not allowed), 1 (for optional), and 2(for mandatory). <br /> <br />|
|TrimLeadingAndTrailingSpacesAndZeroes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether leading and trailing spaces must be trimmed. <br /> <br />|
|ValidateEDITypes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the EDI types must be validated or not. <br /> <br />|
|ValidateXSDTypes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the XSD validation must be performed or not. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

