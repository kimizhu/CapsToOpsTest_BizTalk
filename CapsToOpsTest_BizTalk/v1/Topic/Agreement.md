---
description: na
keywords: na
pagetitle: Agreement
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 44f5e4ed-0863-4687-b3ba-ff6ddc417f37
---
# Agreement
An `Agreement` entity encapsulates agreement information between two business profiles.

- [Agreement Entity Properties](/Topic/Agreement.md#BKMK_AgreementProperties)

- [Create an Agreement](/Topic/Agreement.md#BKMK_CreateAgreement)

- [List Agreements](/Topic/Agreement.md#BKMK_ListAgreements)

- [Update an Agreement](/Topic/Agreement.md#BKMK_UpdateAgreement)

- [Delete an Agreement](/Topic/Agreement.md#BKMK_DeleteAgreement)

- [Link Other Entities with Agreements](/Topic/Agreement.md#BKMK_CreateLink)

- [Delete Link between Other Entities and Agreements](/Topic/Agreement.md#BKMK_DeleteOtherLink)

## <a name="BKMK_AgreementProperties"></a>Agreement Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the agreement. This value is auto-generated. <br /> <br />|
|Name <br /> <br />|String <br /> <br />|**Required**. Specifies a unique name for the agreement. This must not be more than 256 characters. <br /> <br />|
|ProtocolName <br /> <br />|String <br /> <br />|**Required**. Set this to **X12** for an X12 agreement or **AS2** for an AS2 agreement. This value must not be more than 256 characters and is case-insensitive. <br /> <br />|
|Description <br /> <br />|String <br /> <br />|**Required**. Specifies a description for the agreement. This value must not be more than 512 characters. <br /> <br />|
|EnabledInternal <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the agreement is enabled or not. <br /> <br />|
|StartDateInternal <br /> <br />|DateTime <br /> <br />|Specifies the start date for the agreement. <br /> <br />|
|EndDateInternal <br /> <br />|DateTime <br /> <br />|Specifies the end date for the agreement. <br /> <br />|
|Contacts <br /> <br />|DataServiceCollection&lt;Contact&gt; <br /> <br />|A navigation property that references the contact information associated with an agreement. <br /> <br />|
|CustomSettings <br /> <br />|DataServiceCollection&lt;CustomSetting&gt; <br /> <br />|**Required**. A navigation property that references custom information associated with an agreement. <br /> <br />|
|Partnership <br /> <br />|Partnership <br /> <br />|**Required**. A navigation property that references the partnerships this agreement is part of. <br /> <br />|
|OnewayAgreementBtoA <br /> <br />|OnewayAgreement <br /> <br />|**Required**. A navigation property that references the receive side agreement. <br /> <br />|
|OnewayAgreementAtoB <br /> <br />|OnewayAgreement <br /> <br />|**Required**. A navigation property that references the send side agreement. <br /> <br />|
|BusinessProfileA <br /> <br />|BusinessProfile <br /> <br />|**Required**. A navigation property that references the sender profile. <br /> <br />|
|BusinessProfileB <br /> <br />|BusinessProfile <br /> <br />|**Required**. A navigation property that references the receiver profile. <br /> <br />|
|SendProtocolSettings <br /> <br />|ProtocolSettings <br /> <br />|**Required**. A navigation property that references the protocol settings associated with the sender’s profile. <br /> <br />|
|ReceiveProtocolSettings <br /> <br />|ProtocolSettings <br /> <br />|**Required**. A navigation property that references the protocol settings associated with the receiver’s profile. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

### Considerations
An agreement must not be deleted if it is already deployed. Also, if an agreement that was previously deployed using the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] is updated using the REST API, the already deployed agreement will be out of sync with the newly deployed agreement.

## <a name="BKMK_CreateAgreement"></a>Create an Agreement
You can create an agreement using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Agreements <br /> <br />|HTTP/1.1 <br /> <br />|
> [!NOTE]
> You cannot create an agreement without linking it to partnerships and business profiles. In the following sample request, a partnership and business profiles are linked to an agreement using the **&lt;link&gt;** element of the request body.

### Sample Request

```
POST bts_svc_tpm_metadata/Agreements HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.Agreement" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Partnership" type="application/atom+xml;type=entry" title="Partnership" href="https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/Partnerships(1)" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/BusinessProfileA" type="application/atom+xml;type=entry" title="BusinessProfileA" href="https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/BusinessProfiles(1)" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/BusinessProfileB" type="application/atom+xml;type=entry" title="BusinessProfileB" href="https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/BusinessProfiles(2)" />
  <id />
  <title />
  <updated>2013-02-06T05:41:33Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Description m:null="true" />
      <d:EnabledInternal m:type="Edm.Boolean">true</d:EnabledInternal>
      <d:EndDateInternal m:type="Edm.DateTime">2099-01-01T00:00:00</d:EndDateInternal>
      <d:Id m:type="Edm.Int32">0</d:Id>
      <d:Name>Agreement_594</d:Name>
      <d:ProtocolName>X12</d:ProtocolName>
      <d:StartDateInternal m:type="Edm.DateTime">2009-01-01T00:00:00</d:StartDateInternal>
      <d:Version m:type="Edm.Binary">AA==</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListAgreements"></a>List Agreements
You can list an agreement using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Agreements <br /> <br />This returns all the business profiles <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Agreements(*id*) <br /> <br />This returns information about the agreement with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the profiles**

```
GET bts_svc_tpm_metadata/Agreements HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific agreement**

```
GET bts_svc_tpm_metadata/Agreements(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateAgreement"></a>Update an Agreement
You can update an agreement using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Agreements(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/Agreements(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
If-Match: W/"X'00000000000007FD'"
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/Agreements(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.Agreement" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-06T06:24:07Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Description m:null="true" />
      <d:EnabledInternal m:type="Edm.Boolean">true</d:EnabledInternal>
      <d:EndDateInternal m:type="Edm.DateTime">2099-01-01T00:00:00</d:EndDateInternal>
      <d:Id m:type="Edm.Int32">1</d:Id>
      <d:Name>New_Updated_Agreement</d:Name>
      <d:ProtocolName>X12</d:ProtocolName>
      <d:StartDateInternal m:type="Edm.DateTime">2009-01-01T00:00:00</d:StartDateInternal>
      <d:Version m:type="Edm.Binary">AAAAAAAAB/0=</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteAgreement"></a>Delete an Agreement
You can delete an agreement using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Agreements(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/Agreements(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
If-Match: W/"X'0000000000000836'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreateLink"></a>Link Other Entities with Agreements
In [Create an Agreement](/Topic/Agreement.md#BKMK_CreateAgreement) section, we saw how to create a link between an agreement and a partnership, and an agreement and business profiles, while creating an agreement. In this section, we see how to create a link in the opposite direction, for example, from a partnership to an agreement. To create the link, the URI of the agreement must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partnerships(*id*)/$links/Agreements <br /> <br />*Partnerships(id)* denotes the ID of the partnership that links to the agreement <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following sample message shows how to create a link from a Partnership entity to an Agreement entity. You can use similar request messages to create links from other entities (BusinessProfiles, Contact, etc.) to an Agreement entity.

```
POST bts_svc_tpm_metadata/Partnerships(1)/$links/Agreements HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/Agreements(1)</uri>
```

## <a name="BKMK_DeleteOtherLink"></a>Delete Link between Other Entities and Agreements
You can delete a link between other entities, for example a Partnership, and agreements using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partnerships(*id*)/$links/Agreements(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following sample message shows how to delete a link between a partnership and an agreement. You can use similar requests to delete links from other entities (BusinessProfiles, Contacts, etc.) and an agreement.

```
DELETE bts_svc_tpm_metadata/Partnerships(1)/$links/Agreements(1) HTTP/1.1
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

