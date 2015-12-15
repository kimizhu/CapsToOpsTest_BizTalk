---
description: na
keywords: na
pagetitle: QualifierIdentity
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e816f684-fcc3-4753-a412-4fb948035f98
---
# QualifierIdentity
A `QualifierIdentity` entity inherits the `BusinessIdentity` entity and adds identity information specific to a protocol.

- [QualifierIdentity Entity Properties](/Topic/QualifierIdentity.md#BKMK_PartnerProperties)

- [Create a Qualifier Identity](/Topic/QualifierIdentity.md#BKMK_CreateBIdentity)

- [List Qualifier Identities](/Topic/QualifierIdentity.md#BKMK_ListBIdentity)

- [Update a Qualifier Identity](/Topic/QualifierIdentity.md#BKMK_UpdateBIdentity)

- [Delete a Qualifier Identity](/Topic/QualifierIdentity.md#BKMK_DeleteBIdentity)

- [Link Business Profiles with Qualifier Identities](/Topic/QualifierIdentity.md#BKMK_CreateBIdentityLink)

- [Delete Links between Business Profiles and Qualifier Identities](/Topic/QualifierIdentity.md#BKMK_DeleteBIdentityLink)

## <a name="BKMK_PartnerProperties"></a>QualifierIdentity Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|Qualifier <br /> <br />|String <br /> <br />|**Required**. Specifies the qualifier text, such as **ZZ**. The length of the text must not be more than 64 characters. <br /> <br />|
|Description <br /> <br />|String <br /> <br />|Specifies the descriptive text about the qualifier.   The text must not be more than 256 characters. <br /> <br />|
|Value <br /> <br />|String <br /> <br />|**Required**. Specifies the qualifier value. The value must not be more than 256 characters. <br /> <br />|
|SupportedProtocols <br /> <br />|String <br /> <br />|Specifies the supported protocols, such as **X12**. The value must not be more than 256 characters. <br /> <br />|

## <a name="BKMK_CreateBIdentity"></a>Create a Qualifier Identity
You can create a qualifier identity using POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessIdentities <br /> <br />|HTTP/1.1 <br /> <br />|
> [!NOTE]
> You cannot create a business identity without linking it to a business profile or a OneWayAgreement&#42; entity. In the following sample request, a business identity is linked to a business profile using the **&lt;link&gt;** element of the request body.

### Sample Request

```
POST bts_svc_tpm_metadata/BusinessIdentities HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/atom+xml
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.QualifierIdentity" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/BusinessProfile" type="application/atom+xml;type=entry" title="BusinessProfile" href="bts_svc_tpm_metadata/BusinessProfiles(43)" />
  <id />
  <title />
  <updated>2013-01-31T07:25:37Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Description m:null="true" />
      <d:Name>IdentityA_859</d:Name>
      <d:Qualifier>ZZ</d:Qualifier>
      <d:Value>1_859</d:Value>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListBIdentity"></a>List Qualifier Identities
You can list qualifier identities using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessIdentities <br /> <br />This returns all the qualifier identities <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessIdentities(*id*) <br /> <br />This returns information about the qualifier identity with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the identities**

```
GET bts_svc_tpm_metadata/BusinessIdentities HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific identity**

```
GET bts_svc_tpm_metadata/BusinessIdentities(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateBIdentity"></a>Update a Qualifier Identity
You can update a qualifier identity using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessIdentities(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/BusinessIdentities(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/atom+xml
If-Match: W/"X'0000000000001003'"
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/BusinessIdentities(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.QualifierIdentity" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-01-31T07:45:00Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Name>New Identity</d:Name>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteBIdentity"></a>Delete a Qualifier Identity
You can delete a qualifier identity using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessIdentities(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/BusinessIdentities(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
If-Match: W/"X'000000000000101E'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreateBIdentityLink"></a>Link Business Profiles with Qualifier Identities
In the [Create a Qualifier Identity](/Topic/QualifierIdentity.md#BKMK_CreateBIdentity) section, we saw how to create a link between a qualifier identity and a business profile while creating a qualifier identity. In this section, we see how to create a link in the opposite direction, that is, from a business profile to a qualifier identity. The URI of the qualifier identity must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles(*id*)/$links/BusinessIdentities <br /> <br />*BusinessProfiles(id)* denotes the ID of the business profile that links to the qualifier identity <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/BusinessProfiles(1)/$links/BusinessIdentities HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 217
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/BusinessIdentities(1)</uri>
```

## <a name="BKMK_DeleteBIdentityLink"></a>Delete Links between Business Profiles and Qualifier Identities
You can delete a link between business profiles and qualifier identities by using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles(*id*)/$links/BusinessIdentities(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/BusinessProfiles(1)/$links/BusinessIdentities(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

