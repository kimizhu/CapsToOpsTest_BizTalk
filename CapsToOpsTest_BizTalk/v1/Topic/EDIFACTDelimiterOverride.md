---
description: na
keywords: na
pagetitle: EDIFACTDelimiterOverride
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60909fc7-2efa-41bc-9e2a-343827755e97
---
# EDIFACTDelimiterOverride
The `EDIFACTDelimiterOverrides` entity captures the EDIFACT delimiter overrides to be associated with an EDIFACT protocol setting, within an EDIFACT agreement.

- [EDIFACTDelimiterOverrides Entity Properties](/Topic/EDIFACTDelimiterOverride.md#BKMK_Props)

## <a name="BKMK_Props"></a>EDIFACTDelimiterOverrides Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ComponentSeparator <br /> <br />|String <br /> <br />|Specifies a single character component data element separator that separates simple data elements within composite data elements <br /> <br />|
|DataElementSeparator <br /> <br />|String <br /> <br />|Specifies a single character data element separator that separates composite data elements consisting of two or more simple data elements or simple data elements that are not part of a composite. <br /> <br />|
|DecimalPointIndicator <br /> <br />|Short <br /> <br />|Specify whether you want to use a **comma** or **decimal** as the decimal notation to be used in the outgoing interchange. Specify: <br /> <br /><ul><li>**0** for comma </li><li>**1** for decimal </li> </ul>|
|ReleaseIndicator <br /> <br />|String <br /> <br />|Specify a single character that indicates that the following character is not a syntax separator, terminator, or release character, but is part of the original data. <br /> <br />|
|RepetitionSeparator <br /> <br />|String <br /> <br />|Specify a single character that is used to separate segments that repeat within a transaction set. <br /> <br />|
|SegmentTerminator <br /> <br />|String <br /> <br />|Specifies a single character that is used to indicate the end of an EDI segment <br /> <br />|
|SegmentTerminatorSuffix <br /> <br />|Short <br /> <br />|Specifies the suffix used with the segment identifier. If you designate a suffix, the segment terminator data element can be empty. If the segment terminator is left empty, you must designate a suffix. The valid values are: <br /> <br /><ul><li>**0** - None </li><li>**1** - CR </li><li>**2** - LF </li><li>**3** – CR LF </li> </ul>|
|MessageRelease <br /> <br />|String <br /> <br />|Specifies the EDIFACT message release, for example, **10B**, for which the delimiter values are applicable. <br /> <br />|
|MessageVersion <br /> <br />|String <br /> <br />|Specifies the protocol version, for example, **D**, for which the delimiter values are applicable. <br /> <br />|
|MessageId <br /> <br />|String <br /> <br />|Specifies the message ID, for example **INVOIC**, for which the delimiter values are applicable. <br /> <br />|
|TargetNamespace <br /> <br />|String <br /> <br />|Specifies the target namespace string, for example, `http://schemas.microsoft.com/BizTalk/EDI/EDIFACT/2006`. <br /> <br />|

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

