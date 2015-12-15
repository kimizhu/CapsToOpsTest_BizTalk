---
description: na
keywords: na
pagetitle: X12DelimiterOverrides
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be688e7e-5bc4-4f3b-9260-6f1ac637b42d
---
# X12DelimiterOverrides
The `X12DelimiterOverrides` entity captures the X12 delimiter overrides to be associated with an X12 protocol setting, within an X12 agreement.

- [X12DelimiterOverrides Entity Properties](/Topic/X12DelimiterOverrides.md#BKMK_Props)

## <a name="BKMK_Props"></a>X12DelimiterOverrides Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ComponentSeparator <br /> <br />|String <br /> <br />|Specifies a single character that is used to separate composite data elements. Default is (**:**). <br /> <br />|
|DataElementSeparator <br /> <br />|String <br /> <br />|Specifies a single character that is used to separate simple data elements within composite data elements. Default value is (**&#42;**). <br /> <br />|
|ReplaceChar <br /> <br />|String <br /> <br />|Specifies the replace character to be used. Specify this property if the payload data contains characters that are also used as data, segment, or component separators. When generating the outbound X12 message, all instances of separator characters in the payload data will be replaced with the specified character. <br /> <br />|
|ReplaceSeparatorsInPayload <br /> <br />|Bool <br /> <br />|Set this to true if you want the **ReplaceChar** property to be honored. <br /> <br />|
|SegmentTerminator <br /> <br />|String <br /> <br />|Specifies a single character that is used to indicate the end of an EDI segment. Default value is (**~**). <br /> <br />|
|SegmentTerminatorSuffix <br /> <br />|Short <br /> <br />|Specifies the suffix used with the segment identifier. If you designate a suffix, the segment terminator data element can be empty. If the segment terminator is left empty, you must designate a suffix. The valid values are: <br /> <br /><ul><li>**0** - None </li><li>**1** - CR </li><li>**2** - LF </li><li>**3** – CR LF </li> </ul>Default value is **None**. <br /> <br />|
|MessageId <br /> <br />|String <br /> <br />|Specifies the message ID, for example, **810**, for which the delimiter values are applicable <br /> <br />|
|ProtocolVersion <br /> <br />|String <br /> <br />|Specified the protocol version, for example, **00401**, for which the delimiter values are applicable. <br /> <br />|
|TargetNamespace <br /> <br />|String <br /> <br />|Specifies the target namespace string, for example, `http://schemas.microsoft.com/BizTalk/EDI/X12/2006`. <br /> <br />|

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

