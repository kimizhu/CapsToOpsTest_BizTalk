---
description: na
keywords: na
pagetitle: BusinessIdentity
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b45487e-2299-4390-953a-766a2a0f29e8
---
# BusinessIdentity
A `BusinessIdentity` entity defines the X12 identifiers in a profile. A business identity is an abstract entity so it cannot be instantiated. The **QualifierIdentity** entity inherits the **BusinessIdentity**. So, to create a business identity, you must create a **QualifierIdentity** entity. For more information, see [QualifierIdentity](/Topic/QualifierIdentity.md).

- [BusinessIdentity Entity Properties](/Topic/BusinessIdentity.md#BKMK_Properties)

## <a name="BKMK_Properties"></a>BusinessIdentity Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|Name <br /> <br />|String <br /> <br />|**Required**. Specifies a unique name for the identifier. The identifier name must not exceed 256 characters. <br /> <br />|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the identifier. This value is auto-generated. <br /> <br />|
|BusinessProfile <br /> <br />|BusinessProfile <br /> <br />|**Required**. A navigation property that references business profiles to which the business identity belongs. <br /> <br />|
|OnewayAgreementSender <br /> <br />|DataServiceCollection&lt;OnewayAgreement&gt; <br /> <br />|A navigation property that references the send-side one-way agreement. <br /> <br />|
|OnewayAgreementReceiver <br /> <br />|DataServiceCollection&lt;OnewayAgreement&gt; <br /> <br />|A navigation property that references the receive-side one-way agreement. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

