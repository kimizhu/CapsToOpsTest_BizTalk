---
description: na
keywords: na
pagetitle: CustomSetting
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ef34e4b-511d-4ee4-b4c0-f3d4729fa655
---
# CustomSetting
The `CustomSettings` entity provides represents the custom information extending a Partner, BusinessProfile, or an Agreement.

- [CustomSetting Entity Properties](/Topic/CustomSetting.md#BKMK_CustomEntityProps)

- [Create a CustomSetting Entity](/Topic/CustomSetting.md#BKMK_CreateCustomSettings)

- [List CustomSetting](/Topic/CustomSetting.md#BKMK_ListCustomSetting)

- [Update a CustomSetting](/Topic/CustomSetting.md#BKMK_UpdateCustomSetting)

- [Delete a CustomSetting](/Topic/CustomSetting.md#BKMK_DeleteCustomSetting)

- [Link Other Entities with CustomSetting](/Topic/CustomSetting.md#BKMK_CreateLink)

- [Delete Link between Other Entities and CustomSetting](/Topic/CustomSetting.md#BKMK_DeleteLink)

## <a name="BKMK_CustomEntityProps"></a>CustomSetting Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the custom settings. This value is auto-generated. <br /> <br />|
|Agreement <br /> <br />|Agreement <br /> <br />|A navigation property that references the agreement entity with which the custom settings are associated. <br /> <br />|
|Blob <br /> <br />|Byte <br /> <br />|- <br /> <br />|
|BusinessProfile <br /> <br />|BusinessProfile <br /> <br />|A navigation property that references the business profile with which the custom settings are associated. <br /> <br />|
|Name <br /> <br />|Bool <br /> <br />|**Required**. Specifies a name for the custom setting entity. <br /> <br />|
|Partner <br /> <br />|Partner <br /> <br />|A navigation property that references the partner with which the custom settings are associated. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

### Considerations
A `CustomSettings` entity must be associated with either a `Partner`, `BusinessProfile`, or `Agreement` entity. Also, if a `CustomSettings` entity instance is associated with one of these three entities, it cannot be associated with the other entities. For example, if a `CustomSettings` entity instance is associated with the **Partner** entity, it cannot be associated with the `BusinessProfile` or `Agreement` entity.

## <a name="BKMK_CreateCustomSettings"></a>Create a CustomSetting Entity
You can create a custom settings entity using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CustomSettings <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following request message shows how to create a custom setting and link it to a partner entity.

```
POST bts_svc_tpm_metadata/CustomSettings HTTP/1.1
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
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.CustomSetting" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Partner" type="application/atom+xml;type=entry" title="Partner" href="bts_svc_tpm_metadata/Partners(1)" />
  <id />
  <title />
  <updated>2013-02-10T23:58:44Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Blob m:type="Edm.Binary" m:null="true" />
      <d:Id m:type="Edm.Int32">0</d:Id>
      <d:Name>CustomSetting1</d:Name>
      <d:Version m:type="Edm.Binary">AA==</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListCustomSetting"></a>List CustomSetting
You can list custom settings using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CustomSettings <br /> <br />This returns all the custom settings <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CustomSettings(*id*) <br /> <br />This returns information about the custom setting with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the custom settings**

```
GET bts_svc_tpm_metadata/CustomSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific custom setting**

```
GET bts_svc_tpm_metadata/CustomSettings() HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateCustomSetting"></a>Update a CustomSetting
You can update a custom setting using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CustomSettings(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/CustomSettings(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000FA5'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 796
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id> CustomSettings/CustomSettings(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.CustomSetting" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-11T00:09:17Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Blob m:type="Edm.Binary" m:null="true" />
      <d:Id m:type="Edm.Int32">1</d:Id>
      <d:Name>CustomSetting2</d:Name>
      <d:Version m:type="Edm.Binary">AAAAAAAAD6U=</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteCustomSetting"></a>Delete a CustomSetting
You can delete a custom setting using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/CustomSettings(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/CustomSettings(1) HTTP/1.1
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

## <a name="BKMK_CreateLink"></a>Link Other Entities with CustomSetting
In [Create a CustomSetting Entity](/Topic/CustomSetting.md#BKMK_CreateCustomSettings) section, we saw how to create a link between a custom setting and a partner entity while creating the custom setting entity. In this section, we see how to create a link in the opposite direction, that is, from a partner entity to a custom setting. To create the link, the URI of the partner must be included in the request body.

You could use similar requests to create links from Agreement or BusinessProfile entities.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(id)//$links/CustomSettings <br /> <br />*Partners(id)* denotes the ID of the partner that links to the custom setting. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/Partners(1)/$links/CustomSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 213
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/CustomSettings(1)</uri>
```

## <a name="BKMK_DeleteLink"></a>Delete Link between Other Entities and CustomSetting
You can delete a link between other entities and a custom setting by using the HTTP DELETE method. This section shows the request URI and message to delete the link between a partner and a custom setting. You can use a similar request to delete a link from a business profile or an agreement.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/CustomSettings(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/Partners(1)/$links/CustomSettings(1)HTTP/1.1
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

