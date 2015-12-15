---
description: na
keywords: na
pagetitle: Partner
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b7e09b8-5ac5-4d5b-90f2-647d3814093e
---
# Partner
A `Partner` entity represents a trading partner entity. A partner is the most basic building block of a trading partner management solution.

- [Partner Entity Properties](/Topic/Partner.md#BKMK_PartnerProperties)

- [Create a Partner](/Topic/Partner.md#BKMK_CreatePartner)

- [List Partners](/Topic/Partner.md#BKMK_ListPartners)

- [Update a Partner](/Topic/Partner.md#BKMK_UpdatePartner)

- [Delete a Partner](/Topic/Partner.md#BKMK_DeletePartner)

## <a name="BKMK_PartnerProperties"></a>Partner Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|Name <br /> <br />|String <br /> <br />|**Required**. Specifies a unique name for the partner. The partner name must not exceed 256 characters. <br /> <br />|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the partner. This value is auto-generated. <br /> <br />|
|Description <br /> <br />|String <br /> <br />|Specifies a descriptive text for the partner. The text must not exceed 256 characters. <br /> <br />|
|BusinessProfiles <br /> <br />|DataServiceCollection&lt;BusinessProfile&gt; <br /> <br />|A navigation property that references the business profiles associated with the partner. <br /> <br />|
|Contacts <br /> <br />|DataServiceCollection&lt;Contact&gt; <br /> <br />|A navigation property that references the contact details associated with the partner. <br /> <br />|
|CustomSettings <br /> <br />|DataServiceCollection&lt;CustomSetting&gt; <br /> <br />|A navigation property that references the custom information about a partner. <br /> <br />|
|PartnershipsAsA <br /> <br />|DataServiceCollection&lt;Partnership&gt; <br /> <br />|A navigation property that references the sender partnerships. <br /> <br />|
|PartnershipsAsB <br /> <br />|DataServiceCollection&lt;Partnership&gt; <br /> <br />|A navigation property that references the receiver partnerships. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## <a name="BKMK_CreatePartner"></a>Create a Partner
You can create a partner using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/Partners HTTP/1.1
Content-Type: application/atom+xml
Accept: text/html, application/xhtml+xml, */*
Host: integration.zurich.test.dnsdemo1.com:5446
Connection: Keep-Alive
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Authorization: WRAP access_token = "<token>"

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.Partner" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <id />
  <title />
  <updated>2013-01-28T20:35:43Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Name>MyPartner</d:Name>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListPartners"></a>List Partners
You can list partners using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners <br /> <br />This returns information about all the partners <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)] /Partners(*id*) <br /> <br />This returns information about the partner with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the partners**

```
GET bts_svc_tpm_metadata/Partners HTTP/1.1
Accept: text/html, application/xhtml+xml, */*
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
Connection: Keep-Alive
Authorization: WRAP access_token = "<token>"
```
**Retrieve a specific partner**

```
GET bts_svc_tpm_metadata/Partners(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdatePartner"></a>Update a Partner
You can update a partner using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/Partners(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000FB5'"
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/Partners(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.Partner" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-01-28T20:51:19Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Name>NewPartnerxxx</d:Name>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeletePartner"></a>Delete a Partner
You can update a partner using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/Partners(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
If-Match: W/"X'0000000000000FB5'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

