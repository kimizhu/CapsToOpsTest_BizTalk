---
description: na
keywords: na
pagetitle: BusinessProfile
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26a8b2fd-7b7a-4f4a-9089-b74ee9689017
---
# BusinessProfile
A `BusinessProfile` entity represents a business profile attached to a trading partner.

- [BusinessProfile Entity Properties](/Topic/BusinessProfile.md#BKMK_ProfileProperties)

- [Create a Business Profile](/Topic/BusinessProfile.md#BKMK_CreateProfile)

- [List Business Profiles](/Topic/BusinessProfile.md#BKMK_ListProfiles)

- [Update a Business Profile](/Topic/BusinessProfile.md#BKMK_UpdateProfile)

- [Delete a Business Profile](/Topic/BusinessProfile.md#BKMK_DeleteProfile)

- [Link Partners with Business Profiles](/Topic/BusinessProfile.md#BKMK_CreatePartnerLink)

- [Delete Link between Partners and BusinessProfiles](/Topic/BusinessProfile.md#BKMK_DeletePartnerLink)

## <a name="BKMK_ProfileProperties"></a>BusinessProfile Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|Name <br /> <br />|String <br /> <br />|**Required**. Specifies a unique name for the profile. The profile name must not exceed 256 characters. <br /> <br />|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the profile. This value is auto-generated. <br /> <br />|
|Description <br /> <br />|String <br /> <br />|Specifies a descriptive text for the profile. The text must not exceed 512 characters. <br /> <br />|
|Partner <br /> <br />|Partner <br /> <br />|**Required**. A navigation property that references the Partner entity to which the business profile belongs. <br /> <br />|
|BusinessIdentities <br /> <br />|DataServiceCollection&lt;BusinessIdentity&gt; <br /> <br />|A navigation property that references the identities associated with a business profile. <br /> <br />|
|CertificateReferences <br /> <br />|DataServiceCollection&lt;CertificateReference&gt; <br /> <br />|A navigation property that references the certificates associated with a business profile <br /> <br />|
|Contacts <br /> <br />|DataServiceCollection&lt;Contact&gt; <br /> <br />|A navigation property that references the contact details associated with the business profile <br /> <br />|
|CustomSettings <br /> <br />|DataServiceCollection&lt;CustomSetting&gt; <br /> <br />|A navigation property that references the custom information about a business profile. <br /> <br />|
|ProtocolSettings <br /> <br />|DataServiceCollection&lt;ProtocolSettings&gt; <br /> <br />|A navigation property that references the protocol settings for a business profile. <br /> <br />|
|AgreementsAsA <br /> <br />|DataServiceCollection&lt;Agreement&gt; <br /> <br />|A navigation property that references the send-side agreement. <br /> <br />|
|AgreementsAsB <br /> <br />|DataServiceCollection&lt;Agreement&gt; <br /> <br />|A navigation property that references the receive-side agreement. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## <a name="BKMK_CreateProfile"></a>Create a Business Profile
You can create a business profile using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles <br /> <br />|HTTP/1.1 <br /> <br />|
> [!NOTE]
> You cannot create a business profile without linking it to a partner. In the following sample request, a business profile is linked to a partner using the **&lt;link&gt;** element of the request body.

### Sample Request

```
POST bts_svc_tpm_metadata/BusinessProfiles HTTP/1.1
Content-Type: application/json; odata=verbose
Accept: text/html, application/xhtml+xml, */*
Host: integration.zurich.test.dnsdemo1.com:5446
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Connection: Keep-Alive
Authorization: WRAP access_token = "<token>"
Content-Length: 58

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.BusinessProfile" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Partner" type="application/atom+xml;type=entry" title="Partner" href="bts_svc_tpm_metadata/Partners(id)" />
  <id />
  <title />
  <updated>2013-01-28T20:57:26Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>      
      <d:Name>MyProfile</d:Name>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListProfiles"></a>List Business Profiles
You can list business profiles using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles <br /> <br />This returns all the business profiles <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles(*id*) <br /> <br />This returns information about the business profile with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the profiles**

```
GET bts_svc_tpm_metadata/BusinessProfiles HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific profile**

```
GET bts_svc_tpm_metadata/BusinessProfiles(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateProfile"></a>Update a Business Profile
You can update a business profile using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/BusinessProfiles(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000FBB'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 804
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/BusinessProfiles(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.BusinessProfile" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-01-28T23:48:46Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Name>NewProfile123</d:Name>     
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteProfile"></a>Delete a Business Profile
You can delete a business profile using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/BusinessProfiles(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
If-Match: W/"X'0000000000000FD9'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreatePartnerLink"></a>Link Partners with Business Profiles
In [Create a Business Profile](/Topic/BusinessProfile.md#BKMK_CreateProfile) section, we saw how to create a link between a business profile and a partner while creating a business profile. In this section, we see how to create a link in the opposite direction, that is, from a partner to a business profile. To create the link, the URI of the business profile must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/BusinessProfiles <br /> <br />*Partner(id)* denotes the ID of the partner that links to the business profile <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/Partners(1)/$links/BusinessProfiles HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 216
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/BusinessProfiles(1)</uri>
```

## <a name="BKMK_DeletePartnerLink"></a>Delete Link between Partners and BusinessProfiles
You can delete a link between partner and business profile by using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/BusinessProfiles(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/Partners(1)/$links/BusinessProfiles(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 216
Expect: 100-continue
```

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

