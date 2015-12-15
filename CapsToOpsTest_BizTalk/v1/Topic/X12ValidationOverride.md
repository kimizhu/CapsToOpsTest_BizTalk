---
description: na
keywords: na
pagetitle: X12ValidationOverride
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22e375bd-e9f0-4382-93ab-83ddca089ccc
---
# X12ValidationOverride
The `X12ValidationOverrides` entity captures the X12 validation override settings associated with an X12 protocol setting.

- [X12ValidationOverrides Entity Properties](/Topic/X12ValidationOverride.md#BKMK_EntityProps)

- [Create an X12ValidationOverride](/Topic/X12ValidationOverride.md#BKMK_CreateX12ValidOverride)

- [List X12ValidationOverride](/Topic/X12ValidationOverride.md#BKMK_ListX12ValidOverride)

- [Update an X12ValidationOverride](/Topic/X12ValidationOverride.md#BKMK_UpdateX12SchemaRefs)

- [Delete an X12ValidationOverride](/Topic/X12ValidationOverride.md#BKMK_DeleteX12ValidOverride)

- [Link Other Entities with X12ValidationOverride](/Topic/X12ValidationOverride.md#BKMK_CreateLink)

- [Delete Link between Other Entities and X12ValidationOverride](/Topic/X12ValidationOverride.md#BKMK_DeleteLink)

## <a name="BKMK_EntityProps"></a>X12ValidationOverrides Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the X12 validation override. This value is auto-generated. <br /> <br />|
|AllowLeadingAndTrailingSpacesAndZeroes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether leading and trailing spaces must be allowed. <br /> <br />|
|MessageId <br /> <br />|String <br /> <br />|**Required**. Specifies the message ID, such as, **810**. This value must not be a duplicate in the context of the same X12ProtocolSettings. <br /> <br />|
|X12ProtocolSettings <br /> <br />|X12ProtocolSettings <br /> <br />|**Required**. A navigation property that references the X12 protocol settings associated with the overrides. <br /> <br />|
|X12ProtocolSettingsId <br /> <br />|Int <br /> <br />|**Required**. A navigation property that references an X12 protocol settings ID. <br /> <br />|
|SeparatorPolicy <br /> <br />|Int <br /> <br />|**Required**. Specifies the separator policy. The possible values are 0 (for not allowed), 1 (for optional), and 2(for mandatory). <br /> <br />|
|ValidateCharacterSet <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the character set must be validated or not. <br /> <br />|
|ValidateEDITypes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the EDI types must be validated or not. <br /> <br />|
|ValidateXSDTypes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the XSD validation must be performed or not. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## <a name="BKMK_CreateX12ValidOverride"></a>Create an X12ValidationOverride
You can create an X12 validation override entity using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12ValidationOverrides <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following request message shows how to create an X12 validation override entity and link it to X12ProtocoSetting entity.

```
POST bts_svc_tpm_metadata/X12ValidationOverrides HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 1446
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.X12ValidationOverride" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/X12ProtocolSettings" type="application/atom+xml;type=entry" title="X12ProtocolSettings" href="bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings" />
  <id />
  <title />
  <updated>2013-02-10T23:00:50Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:AllowLeadingAndTrailingSpacesAndZeroes m:type="Edm.Boolean">true</d:AllowLeadingAndTrailingSpacesAndZeroes>
      <d:Id m:type="Edm.Int32">0</d:Id>
      <d:MessageId>810</d:MessageId>
      <d:SeparatorPolicy m:type="Edm.Int16">2</d:SeparatorPolicy>
      <d:ValidateCharacterSet m:type="Edm.Boolean">true</d:ValidateCharacterSet>
      <d:ValidateEDITypes m:type="Edm.Boolean">true</d:ValidateEDITypes>
      <d:ValidateXSDTypes m:type="Edm.Boolean">true</d:ValidateXSDTypes>
      <d:Version m:type="Edm.Binary">AA==</d:Version>
      <d:X12ProtocolSettingsId m:type="Edm.Int32">0</d:X12ProtocolSettingsId>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListX12ValidOverride"></a>List X12ValidationOverride
You can list X12 validation overrides using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12ValidationOverrides <br /> <br />This returns all the X12 validation overrides <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12ValidationOverrides(*id*) <br /> <br />This returns information about the X12 validation override with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the X12 validation overrides**

```
GET bts_svc_tpm_metadata/X12ValidationOverrides HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific X12 validation override**

```
GET bts_svc_tpm_metadata/X12ValidationOverrides(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateX12SchemaRefs"></a>Update an X12ValidationOverride
You can update an X12 validation override using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12ValidationOverrides(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/X12ValidationOverrides(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000FA3'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 1217
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/X12ValidationOverrides(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.X12ValidationOverride" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-10T23:13:39Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:AllowLeadingAndTrailingSpacesAndZeroes m:type="Edm.Boolean">true</d:AllowLeadingAndTrailingSpacesAndZeroes>
      <d:Id m:type="Edm.Int32">1</d:Id>
      <d:MessageId>810</d:MessageId>
      <d:SeparatorPolicy m:type="Edm.Int16">2</d:SeparatorPolicy>
      <d:ValidateCharacterSet m:type="Edm.Boolean">false</d:ValidateCharacterSet>
      <d:ValidateEDITypes m:type="Edm.Boolean">false</d:ValidateEDITypes>
      <d:ValidateXSDTypes m:type="Edm.Boolean">false</d:ValidateXSDTypes>
      <d:Version m:type="Edm.Binary">AAAAAAAAD6M=</d:Version>
      <d:X12ProtocolSettingsId m:type="Edm.Int32">11</d:X12ProtocolSettingsId>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteX12ValidOverride"></a>Delete an X12ValidationOverride
You can delete an X12 validation override using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12ValidationOverrides(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/X12ValidationOverrides(1) HTTP/1.1
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

## <a name="BKMK_CreateLink"></a>Link Other Entities with X12ValidationOverride
In [Create an X12ValidationOverride](/Topic/X12ValidationOverride.md#BKMK_CreateX12ValidOverride) section, we saw how to create a link between an X12 validation override and an X12 protocol settings entity while creating the X12 validation override entity. In this section, we see how to create a link in the opposite direction, that is, from an X12 protocol setting entity to an X12 validation override. To create the link, the URI of the X12 validation override must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(id)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/ValidationOverrides <br /> <br />*ProtocolSettings(id)* denotes the ID of the protocol setting that links to the X12 validation override. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/ProtocolSettings(1)/
Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/ValidationOverrides HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 221
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/X12ValidationOverrides(1)</uri>
```

## <a name="BKMK_DeleteLink"></a>Delete Link between Other Entities and X12ValidationOverride
You can delete a link between other entities and an X12 validation override by using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(*id*)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/ValidationOverrides(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/ProtocolSettings(1)/
Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/ValidationOverrides(1)
HTTP/1.1
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

