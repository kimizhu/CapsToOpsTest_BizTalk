---
description: na
keywords: na
pagetitle: EDIFACTSchemaReference
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 53e73ab5-0143-40d8-8d55-3f67f4b14ae8
---
# EDIFACTSchemaReference
The `EDIFACTSchemaReferences` entity references the schemas that are associated with an EDIFACT protocol setting.

## <a name="BKMK_EntityProperties"></a>EDIFACTSchemaReferences Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the EDIFACT schema reference. This value is auto-generated. <br /> <br />|
|AssociationAssignedCode <br /> <br />|String <br /> <br />|Required. This is derived from the schema. <br /> <br />|
|MessageId <br /> <br />|String <br /> <br />|**Required**. This is derived from the schema. <br /> <br />|
|MessageVersion <br /> <br />||**Required**. This is derived from the schema. <br /> <br />|
|MessageRelease <br /> <br />||**Required**. This is derived from the schema. <br /> <br />|
|SenderApplicationId <br /> <br />|String <br /> <br />|Specifies the sender application ID (UNG2.1). <br /> <br />|
|SenderApplicationQualifier <br /> <br />||Specifies the sender application qualifier (UNG2.2). <br /> <br />|
|SchemaPath <br /> <br />|String <br /> <br />|**Required**. Specifies the path of the schema in the artifact store, such as, **/EFACT_D98A_APERAK.XSD**. This must not be more than 230 characters. <br /> <br />|
|EDIFACTProtocolSettings <br /> <br />|EDIFACTProtocolSettings <br /> <br />|**Required**. A navigation property that references the EDIFACT protocol settings associated with the schema reference. <br /> <br />|
|EDIFACTProtocolSettingsId <br /> <br />|Int <br /> <br />|**Required**. Specifies the EDIFACT protocol settings ID. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

