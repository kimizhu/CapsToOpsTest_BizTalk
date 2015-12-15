---
description: na
keywords: na
pagetitle: CertificateReference
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 884e8dc3-022d-4a32-a5e5-c8f3b724bf14
---
# CertificateReference
A `CertificateReference` entity refers to a certificate in the artifact store and is used for configuring AS2 agreements.

- [CertificateReference Entity Properties](/Topic/CertificateReference.md#BKMK_EntryProps)

- [Create a CertificateReference](/Topic/CertificateReference.md#BKMK_CreateCert)

- [List CertificateReferences](/Topic/CertificateReference.md#BKMK_ListCerts)

- [Update a CertificateReference](/Topic/CertificateReference.md#BKMK_UpdateCert)

- [Delete a CertificateReference](/Topic/CertificateReference.md#BKMK_DeleteCertRef)

- [Link Other Entities with CertificateReference](/Topic/CertificateReference.md#BKMK_CreateLink)

- [Delete Link between Other Entities and CertificateReference](/Topic/CertificateReference.md#BKMK_DeleteSchemaRefLink)

## <a name="BKMK_EntryProps"></a>CertificateReference Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the certificate reference. This value is auto-generated. <br /> <br />|
|Thumbprint <br /> <br />|String <br /> <br />|**Required**. Specifies the unique thumbprint of the certificate. This must not be more than 128 characters. <br /> <br />|
|AS2ProtocolSettingsForEncryption <br /> <br />|DataServiceCollection&lt;AS2ProtocolSettings&gt; <br /> <br />|A navigation property that references the AS2 protocol settings for encryption. <br /> <br />|
|AS2ProtocolSettingsForSigning <br /> <br />|DataServiceCollection&lt;AS2ProtocolSettings&gt; <br /> <br />|A navigation property that references the AS2 protocol settings for signing. <br /> <br />|
|BusinessProfile <br /> <br />|BusinessProfile <br /> <br />|**Required**. A navigation property that references the business profile with which the certificate must be associated. <br /> <br />|
|BusinessProfileId <br /> <br />|Int <br /> <br />|Specifies the ID of the business profile. <br /> <br />|
|HasPrivateKey <br /> <br />|Bool <br /> <br />|Specifies whether the certificate has a private key <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

### Considerations
You must add a certificate reference until you upload the certificate using the artifact store API for uploading the certificate.

## <a name="BKMK_CreateCert"></a>Create a CertificateReference
You can create a certificate reference using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CertificateReferences <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following request message shows how to create a certificate reference and link it to a business profile entity.

```
POST bts_svc_tpm_metadata/CertificateReferences HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.CertificateReference" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/BusinessProfile" type="application/atom+xml;type=entry" title="BusinessProfile" href="bts_svc_tpm_metadata/BusinessProfiles(1)" />
  <id />
  <title />
  <updated>2013-02-13T20:46:45Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:BusinessProfileId m:type="Edm.Int32">0</d:BusinessProfileId>
      <d:HasPrivateKey m:type="Edm.Boolean">false</d:HasPrivateKey>
      <d:Id m:type="Edm.Int32">0</d:Id>
      <d:Thumbprint m:null="true" />
      <d:Version m:type="Edm.Binary">AA==</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListCerts"></a>List CertificateReferences
You can list the certificate references using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CertificateReferences <br /> <br />This returns all the certificate reference entities <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CertificateReferences(*id*) <br /> <br />This returns information about the certificate reference with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the certificate references**

```
GET bts_svc_tpm_metadata/CertificateReferences HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific certificate reference**

```
GET bts_svc_tpm_metadata/CertificateReferences(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateCert"></a>Update a CertificateReference
You can update a certificate reference using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CertificateReferences(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/CertificateReferences(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000FDB'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 888
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/CertificateReferences(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.CertificateReference" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-13T21:41:09Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:BusinessProfileId m:type="Edm.Int32">1</d:BusinessProfileId>
      <d:HasPrivateKey m:type="Edm.Boolean">true</d:HasPrivateKey>
      <d:Id m:type="Edm.Int32">1</d:Id>
      <d:Thumbprint m:null="true" />
      <d:Version m:type="Edm.Binary">AAAAAAAAD9s=</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteCertRef"></a>Delete a CertificateReference
You can delete a certificate reference using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CertificateReferences(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/CertificateReferences(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreateLink"></a>Link Other Entities with CertificateReference
In [Create a CertificateReference](/Topic/CertificateReference.md#BKMK_CreateCert) we see how to create a link between a certificate reference and a business profile while creating the certificate reference. In this section, we see how to create a link in the opposite direction, that is, from a business profile to a certificate reference. To create the link, the URI of the certificate reference must be included in the request body. You can use a similar request message to create links from other entities to a certificate reference.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles(id)/$links/CertificateReferences <br /> <br />*BusinessProfiles(id)* denotes the ID of the business profile that links to the certificate reference. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/BusinessProfiles(1)/$links/CertificateReferences HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 220
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/CertificateReferences(1)</uri>
```

## <a name="BKMK_DeleteSchemaRefLink"></a>Delete Link between Other Entities and CertificateReference
You can delete a link between other entities and a certificate reference using a DELETE HTTP method. This section shows how to delete links between a business profile and a certificate reference. You can use similar requests to delete links from other entities to a certificate reference.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BusinessProfiles(id)/$links/CertificateReferences(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/BusinessProfiles(1)/$links/CertificateReferences(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue
```

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

