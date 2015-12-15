---
description: na
keywords: na
pagetitle: X12EnvelopeOverride
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f537d771-cdbf-40ee-a32f-7d0289369d97
---
# X12EnvelopeOverride
The `X12EnvelopeOverrides` entity captures the X12 envelope override settings associated with an X12 protocol setting.

- [X12EnvelopeOverrides Entity Properties](/Topic/X12EnvelopeOverride.md#BKMK_CreateEntity)

- [Create an X12EnvelopeOverride](/Topic/X12EnvelopeOverride.md#BKMK_CreateX12Overrides)

- [List X12EnvelopOverrides](/Topic/X12EnvelopeOverride.md#BKMK_ListX12Overrides)

- [Update an X12EnvelopeOverride](/Topic/X12EnvelopeOverride.md#BKMK_UpdateX12SchemaRefs)

- [Delete an X12EnvelopeOverride](/Topic/X12EnvelopeOverride.md#BKMK_DeleteX12Override)

- [Link Other Entities with X12EnvelopeOverride](/Topic/X12EnvelopeOverride.md#BKMK_CreateLink)

- [Delete Link between Other Entities and X12EnvelopeOverride](/Topic/X12EnvelopeOverride.md#BKMK_DeleteLink)

## <a name="BKMK_CreateEntity"></a>X12EnvelopeOverrides Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the X12 envelope overrides settings. This value is auto-generated. <br /> <br />|
|DateFormat <br /> <br />|Short <br /> <br />|**Required**. Specifies the date format (GS04). The possible values are **CCYYMMDD** or **YYMMDD**. <br /> <br />|
|TimeFormat <br /> <br />|Short <br /> <br />|Required. Specifies the time format. <br /> <br />|
|FunctionalIdentifierCode <br /> <br />|String <br /> <br />|Specifies the functional identifier code (GS01). The possible values are between **AA** to **ZZ**. <br /> <br />|
|HeaderVersion <br /> <br />|String <br /> <br />|- <br /> <br />|
|MessageId <br /> <br />|String <br /> <br />|**Required**. Specifies the message ID, for example, **810**. <br /> <br />|
|ProtocolVersion <br /> <br />|String <br /> <br />|Specified the protocol version, for example, **00401**. <br /> <br />|
|ResponsibleAgencyCode <br /> <br />|Short <br /> <br />|**Required**. Specifies the agency code. The valid values are 84 (for *TransportationDataCoordinationCommittee*) and 88 (for *AccreditedStandardsCommittee*). <br /> <br />|
|ReceiverApplicationId <br /> <br />|String <br /> <br />|Specifies the receiver application ID (GS03). <br /> <br />|
|SenderApplicationId <br /> <br />|String <br /> <br />|Specifies the sender application ID (GS02). <br /> <br />|
|X12ProtocolSettings <br /> <br />|X12ProtocolSettings <br /> <br />|**Required**. A navigation property that references the X12 protocol settings associated with the overrides. <br /> <br />|
|X12ProtocolSettingsId <br /> <br />|Int <br /> <br />|**Required**. A navigation property that references an X12 protocol settings ID. <br /> <br />|
|TargetNamespace <br /> <br />|String <br /> <br />|Specifies the target namespace string, for example, **http://schemas.microsoft.com/BizTalk/EDI/X12/2006**. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## <a name="BKMK_CreateX12Overrides"></a>Create an X12EnvelopeOverride
You can create an X12 envelop override entity using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12EnvelopeOverrides <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following request message shows how to create an X12 envelope override and link it to X12ProtocoSettings entity.

```
POST bts_svc_tpm_metadata/X12EnvelopeOverrides HTTP/1.1
Content-Type: application/json; odata=verbose
Accept: text/html, application/xhtml+xml, */*
Host: integration.zurich.test.dnsdemo1.com:5446
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Connection: Keep-Alive
Authorization: WRAP access_token = "<token>"

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.X12EnvelopeOverride" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/X12ProtocolSettings" type="application/atom+xml;type=entry" title="X12ProtocolSettings" href="bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings" />
  <id />
  <title />
  <updated>2013-02-08T20:59:46Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:DateFormat m:type="Edm.Int16">0</d:DateFormat>
      <d:FunctionalIdentifierCode m:null="true" />
      <d:HeaderVersion>Version</d:HeaderVersion>
      <d:Id m:type="Edm.Int32">0</d:Id>
      <d:MessageId>810</d:MessageId>
      <d:ProtocolVersion>00401</d:ProtocolVersion>
      <d:ReceiverApplicationId>RECEIVE-APP</d:ReceiverApplicationId>
      <d:ResponsibleAgencyCode m:type="Edm.Int16">88</d:ResponsibleAgencyCode>
      <d:SenderApplicationId>BTS-SENDER2</d:SenderApplicationId>
      <d:TargetNamespace>http://schemas.microsoft.com/BizTalk/EDI/X12/2006</d:TargetNamespace>
      <d:TimeFormat m:type="Edm.Int16">0</d:TimeFormat>
      <d:Version m:type="Edm.Binary">AA==</d:Version>
      <d:X12ProtocolSettingsId m:type="Edm.Int32">0</d:X12ProtocolSettingsId>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListX12Overrides"></a>List X12EnvelopOverrides
You can list X12 envelope overrides using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12EnvelopeOverrides <br /> <br />This returns all the X12 envelope overrides <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12EnvelopeOverrides(*id*) <br /> <br />This returns information about the X12 envelope override with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the X12 envelope overrides**

```
GET bts_svc_tpm_metadata/X12EnvelopeOverrides HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific X12 envelope override**

```
GET bts_svc_tpm_metadata/X12EnvelopeOverrides(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateX12SchemaRefs"></a>Update an X12EnvelopeOverride
You can update an X12 envelop override using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12EnvelopeOverrides(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/X12EnvelopeOverrides(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000A67'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 1344
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/X12EnvelopeOverrides(6)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.X12EnvelopeOverride" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-10T22:30:44Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:DateFormat m:type="Edm.Int16">0</d:DateFormat>
      <d:FunctionalIdentifierCode m:null="true" />
      <d:HeaderVersion>Version1</d:HeaderVersion>
      <d:Id m:type="Edm.Int32">6</d:Id>
      <d:MessageId>840</d:MessageId>
      <d:ProtocolVersion>00401</d:ProtocolVersion>
      <d:ReceiverApplicationId>RECEIVE-APP</d:ReceiverApplicationId>
      <d:ResponsibleAgencyCode m:type="Edm.Int16">88</d:ResponsibleAgencyCode>
      <d:SenderApplicationId>BTS-SENDER2</d:SenderApplicationId>
      <d:TargetNamespace>http://schemas.microsoft.com/BizTalk/EDI/X12/2006</d:TargetNamespace>
      <d:TimeFormat m:type="Edm.Int16">0</d:TimeFormat>
      <d:Version m:type="Edm.Binary">AAAAAAAACmc=</d:Version>
      <d:X12ProtocolSettingsId m:type="Edm.Int32">13</d:X12ProtocolSettingsId>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteX12Override"></a>Delete an X12EnvelopeOverride
You can delete an X12 envelope override using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/X12EnvelopeOverrides(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/X12EnvelopeOverrides(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
If-Match: W/"X'0000000000000A66'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreateLink"></a>Link Other Entities with X12EnvelopeOverride
In [Create an X12EnvelopeOverride](/Topic/X12EnvelopeOverride.md#BKMK_CreateX12Overrides) section, we saw how to create a link between an X12 envelope override and an X12 protocol settings entity while creating the X12 envelope override entity. In this section, we see how to create a link in the opposite direction, that is, from an X12 protocol setting entity to an X12 envelope override. To create the link, the URI of the X12 envelope override must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(id)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/EnvelopeOverrides <br /> <br />*ProtocolSettings(id)* denotes the ID of the protocol setting that links to the X12 envelope override. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/EnvelopeOverrides HTTP/1.1
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 216
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/X12EnvelopeOverrides(1)</uri>
```

## <a name="BKMK_DeleteLink"></a>Delete Link between Other Entities and X12EnvelopeOverride
You can delete a link between other entities and an X12 envelope override by using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(*id*)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/EnvelopeOverrides(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/EnvelopeOverrides(1) HTTP/1.1
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

