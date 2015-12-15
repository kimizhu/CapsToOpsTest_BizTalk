---
description: na
keywords: na
pagetitle: OnewayAgreement
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23c0605c-b491-4e77-8970-d7f05549f68d
---
# OnewayAgreement
The `OneWayAgreement` entity captures information for either send or receive side of an agreement.

- [OnewayAgreement Entity Properties](/Topic/OnewayAgreement.md#BKMK_EntityProperties)

- [Create a OnewayAgreement](/Topic/OnewayAgreement.md#BKMK_CreateOneWayAgr)

- [List OnewayAgreements](/Topic/OnewayAgreement.md#BKMK_ListOneWay)

- [Update a OnewayAgreement](/Topic/OnewayAgreement.md#BKMK_UpdateOneWay)

- [Delete a OnewayAgreement](/Topic/OnewayAgreement.md#BKMK_DeleteOneWayAgr)

- [Link Other Entities with OnewayAgreements](/Topic/OnewayAgreement.md#BKMK_CreateLink)

- [Delete Link between Other Entities and OnewayAgreements](/Topic/OnewayAgreement.md#BKMK_DeleteLink)

## <a name="BKMK_EntityProperties"></a>OnewayAgreement Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the one-way agreement. This value is auto-generated. <br /> <br />|
|AgreementAsAtoB <br /> <br />|Agreement <br /> <br />|A navigation property that specifies the send-side agreement. <br /> <br />|
|AgreementAsBtoA <br /> <br />|Agreement <br /> <br />|A navigation property that specifies the receive-side agreement. <br /> <br />|
|BatchDescriptions <br /> <br />|DataServiceCollection&lt;BatchDescription&gt; <br /> <br />|A navigation property that references the batch configuration if the one-way agreement is send-side. <br /> <br />|
|ProtocolSettings <br /> <br />|ProtocolSettings <br /> <br />|**Required**. A navigation property that references the protocol settings. <br /> <br />|
|ReceiverBusinessIdentity <br /> <br />|BusinessIdentity <br /> <br />|**Required**. A navigation property that references the receiver ID of the one-way agreement. <br /> <br />|
|SenderBusinessIdentity <br /> <br />|BusinessIdentity <br /> <br />|**Required**. A navigation property that references the sender ID of the one-way agreement. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

### Considerations
A `OnewayAgreement` entity must be associated with either a `ProtocoSetting`, `AgreementSender`, or `AgreementReceiver`.

## <a name="BKMK_CreateOneWayAgr"></a>Create a OnewayAgreement
You can create a one way agreement using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/OnewayAgreements <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following request message shows how to create a one-way agreement and link it to business identities.

```
POST bts_svc_tpm_metadata/OnewayAgreements HTTP/1.1
Content-Type: application/json; odata=verbose
Accept: text/html, application/xhtml+xml, */*
Host: integration.zurich.test.dnsdemo1.com:5446
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Connection: Keep-Alive
Authorization: WRAP access_token = "<token>"

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.OnewayAgreement" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/SenderBusinessIdentity" type="application/atom+xml;type=entry" title="SenderBusinessIdentity" href="https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/BusinessIdentities(1)" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/ReceiverBusinessIdentity" type="application/atom+xml;type=entry" title="ReceiverBusinessIdentity" href="https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/BusinessIdentities(2)" />
  <id />
  <title />
  <updated>2013-02-07T00:43:49Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Id m:type="Edm.Int32">0</d:Id>
      <d:Version m:type="Edm.Binary">AA==</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListOneWay"></a>List OnewayAgreements
You can list one way agreements using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/OnewayAgreements <br /> <br />This returns all the one way agreements <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/OnewayAgreements(*id*) <br /> <br />This returns information about the one-way agreements with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the one-way agreements**

```
GET bts_svc_tpm_metadata/OnewayAgreements HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific one-way agreement**

```
GET bts_svc_tpm_metadata/OnewayAgreements(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateOneWay"></a>Update a OnewayAgreement
You can update a one-way agreement using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/OnewayAgreements(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/OnewayAgreements(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000830'"
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/OnewayAgreements(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.OnewayAgreement" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-07T07:39:56Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Id m:type="Edm.Int32">5</d:Id>
      <d:Version m:type="Edm.Binary">AAAAAAAACDA=</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteOneWayAgr"></a>Delete a OnewayAgreement
You cannot delete a one-way agreement on it’s own. You must instead delete the agreement entity to which the one-way agreement is associated with. For instructions on deleting an agreement, see [Delete an Agreement](/Topic/Agreement.md#BKMK_DeleteAgreement).

## <a name="BKMK_CreateLink"></a>Link Other Entities with OnewayAgreements
In [Create a OneWayAgreement](/Topic/OnewayAgreement.md#BKMK_CreateOneWayAgr) section, we saw how to create a link between a one-way agreement and an agreement while creating the one-way agreement. In this section, we see how to create a link in the opposite direction, that is, from an agreement to a one-way agreement. To create the link, the URI of the one-way agreement must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Agreements(*id*)/$links/OnewayAgreementAToB <br /> <br />*Agreements(id)* denotes the ID of the agreement that links to the one-way agreement <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/Agreements(1)/$links/OnewayAgreementAToB HTTP/1.1
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

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/OnewayAgreements(1)</uri>
```

## <a name="BKMK_DeleteLink"></a>Delete Link between Other Entities and OnewayAgreements
You can delete a link between other entities and a one-way agreement by using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Agreements(*id*)/$links/OnewayAgreementAToB(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/Agreements(1)/$links/OnewayAgreementAToB(1) HTTP/1.1
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

