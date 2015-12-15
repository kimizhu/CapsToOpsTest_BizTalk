---
description: na
keywords: na
pagetitle: X12SchemaReference
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 569b83d8-251a-4d88-9669-c8070a03f53c
---
# X12SchemaReference
The `X12SchemaReferences` entity references the schemas that are associated with an X12 protocol setting.

- [X12SchemaReferences Entity Properties](/Topic/X12SchemaReference.md#BKMK_EntityProperties)

- [Create an X12SchemaReference](/Topic/X12SchemaReference.md#BKMK_CreateX12SchemaRef)

- [List X12SchemaReference](/Topic/X12SchemaReference.md#BKMK_ListX12SchemaRef)

- [Update an X12SchemaReference](/Topic/X12SchemaReference.md#BKMK_UpdateX12SchemaRefs)

- [Delete an X12SchemaReference](/Topic/X12SchemaReference.md#BKMK_DeleteX12SchemaRefs)

- [Link Other Entities with X12SchemaReference](/Topic/X12SchemaReference.md#BKMK_CreateLink)

- [Delete Link between Other Entities and X12SchemaReference](/Topic/X12SchemaReference.md#BKMK_DeleteLink)

## <a name="BKMK_EntityProperties"></a>X12SchemaReferences Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the X12 schema reference. This value is auto-generated. <br /> <br />|
|MessageId <br /> <br />|String <br /> <br />|**Required**. Specifies the message ID, for example, **810**. This must not be more than 15 characters. <br /> <br />|
|SchemaPath <br /> <br />|String <br /> <br />|**Required**. Specifies the path of the schema in the artifact store, such as, **/X12_00401_810.XSD**. This must not be more than 230 characters. <br /> <br />|
|SchemaVersion <br /> <br />|String <br /> <br />|**Required**. Specifies the schema version, such as, **00401**. This must not be more than 15 characters. <br /> <br />|
|SenderApplicationId <br /> <br />|String <br /> <br />|Specifies the sender application ID (GS02). <br /> <br />|
|X12ProtocolSettings <br /> <br />|X12ProtocolSettings <br /> <br />|**Required**. A navigation property that references the X12 protocol settings associated with the schema reference. <br /> <br />|
|X12ProtocolSettingsId <br /> <br />|Int <br /> <br />|**Required**. A navigation property that references an X12 protocol settings ID. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

### Considerations
You can create an X12SchemaReference entity only if a schema is already uploaded to the artifact store.

## <a name="BKMK_CreateX12SchemaRef"></a>Create an X12SchemaReference
You can create an X12 schema reference entity using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12SchemaReferences <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following request message shows how to create an X12 schema reference and link it to X12ProtocoSetting entity.

```
POST bts_svc_tpm_metadata/X12SchemaReferences HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 1194
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.X12SchemaReference" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/X12ProtocolSettings" type="application/atom+xml;type=entry" title="X12ProtocolSettings" href="bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings" />
  <id />
  <title />
  <updated>2013-02-08T23:31:56Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Id m:type="Edm.Int32">0</d:Id>
      <d:MessageId>810</d:MessageId>
      <d:SchemaPath>/X12_00401_810.XSD</d:SchemaPath>
      <d:SchemaVersion>00401</d:SchemaVersion>
      <d:SenderApplicationId m:null="true" />
      <d:Version m:type="Edm.Binary">AA==</d:Version>
      <d:X12ProtocolSettingsId m:type="Edm.Int32">0</d:X12ProtocolSettingsId>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListX12SchemaRef"></a>List X12SchemaReference
You can list X12 schema references using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12SchemaReferences <br /> <br />This returns all the X12 schema reference <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12SchemaReferences(*id*) <br /> <br />This returns information about the X12 schema reference with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the X12 schema references**

```
GET bts_svc_tpm_metadata/X12SchemaReferences HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific X12 schema reference**

```
GET bts_svc_tpm_metadata/X12SchemaReferences(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateX12SchemaRefs"></a>Update an X12SchemaReference
You can update an X12 schema reference using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12SchemaReferences(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/X12SchemaReferences(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000888'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 959
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/X12SchemaReferences(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.X12SchemaReference" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-09T01:31:46Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Id m:type="Edm.Int32">3</d:Id>
      <d:MessageId>840</d:MessageId>
      <d:SchemaPath>/X12_00401_810.XSD</d:SchemaPath>
      <d:SchemaVersion>00401</d:SchemaVersion>
      <d:SenderApplicationId m:null="true" />
      <d:Version m:type="Edm.Binary">AAAAAAAACIg=</d:Version>
      <d:X12ProtocolSettingsId m:type="Edm.Int32">35</d:X12ProtocolSettingsId>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteX12SchemaRefs"></a>Delete an X12SchemaReference
You can delete an X12 schema reference using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12SchemaReferences(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/X12SchemaReferences(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
If-Match: W/"X'0000000000000A69'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreateLink"></a>Link Other Entities with X12SchemaReference
In [Create an X12SchemaReference](/Topic/X12SchemaReference.md#BKMK_CreateX12SchemaRef) section, we saw how to create a link between an X12 schema reference and an X12 protocol settings entity while creating the X12 schema reference entity. In this section, we see how to create a link in the opposite direction, that is, from an X12 protocol setting entity to an X12 schema reference. To create the link, the URI of the X12 schema reference must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(id)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/SchemaReferences <br /> <br />*ProtocolSettings(id)* denotes the ID of the protocol setting that links to the X12 schema reference. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/SchemaReferences HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 219
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/X12SchemaReferences(1)</uri>
```

## <a name="BKMK_DeleteLink"></a>Delete Link between Other Entities and X12SchemaReference
You can delete a link between other entities and an X12 schema reference by using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(*id*)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/SchemaReferences(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/SchemaReferences(1) HTTP/1.1
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

