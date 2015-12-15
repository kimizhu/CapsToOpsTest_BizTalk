---
description: na
keywords: na
pagetitle: Partnership
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b40ed24-4789-4bf2-a649-d7a30746d390
---
# Partnership
A `Partnership` entity represents a partnership between two partners.

- [Partnership Entity Properties](/Topic/Partnership.md#BKMK_PartnershipProperties)

- [Create a Partnership](/Topic/Partnership.md#BKMK_CreatePartnership)

- [List Partnerships](/Topic/Partnership.md#BKMK_ListPartnership)

- [Update a Partnership](/Topic/Partnership.md#BKMK_UpdatePartnership)

- [Delete a Partnership](/Topic/Partnership.md#BKMK_DeletePartnership)

- [Link Partners with Partnerships](/Topic/Partnership.md#BKMK_CreateLinkWithPartner)

- [Delete Link between Partners and Partnerships](/Topic/Partnership.md#BKMK_DeletePartnershipsLink)

## <a name="BKMK_PartnershipProperties"></a>Partnership Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the partnership. This value is auto-generated. <br /> <br />|
|Agreements <br /> <br />|DataServiceCollection&lt;Agreement&gt; <br /> <br />|A navigation property that references the agreement between two partners that are part of a partnership. <br /> <br />|
|PartnerA <br /> <br />|Partner <br /> <br />|A navigation property that references a partner in a partnership. <br /> <br />|
|PartnerB <br /> <br />|Partner <br /> <br />|A navigation property that references the other partner in the partnership. <br /> <br />|

## <a name="BKMK_CreatePartnership"></a>Create a Partnership
You can create a partnership using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partnerships <br /> <br />|HTTP/1.1 <br /> <br />|
> [!NOTE]
> You cannot create a partnership without linking it to the two partners. In the following sample request, a partnership is linked to the partners using the **&lt;link&gt;** element of the request body.

### Sample Request

```
POST bts_svc_tpm_metadata/Partnerships HTTP/1.1
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
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.Partnership" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/PartnerA" type="application/atom+xml;type=entry" title="PartnerA" href="https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/Partners(1)" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/PartnerB" type="application/atom+xml;type=entry" title="PartnerB" href="https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/Partners(2)" />
  <id />
  <title />
  <updated>2013-02-01T23:46:24Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:Id m:type="Edm.Int32">0</d:Id>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListPartnership"></a>List Partnerships
You can list partnerships using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partnerships <br /> <br />This returns all the business partnerships <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partnerships(*id*) <br /> <br />This returns information about the partnership with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the partnerships**

```
GET bts_svc_tpm_metadata/Partnerships() HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific partnership**

```
GET bts_svc_tpm_metadata/Partnerships(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdatePartnership"></a>Update a Partnership
Updating a partnership means updating the links between the Partnership and Partner entities. You can update the links by passing the URI of the partner as part of the request body and using the PUT HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|PUT <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partnerships(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
PUT bts_svc_tpm_metadata/Partnerships(1)/$links/PartnerA HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/Partners(3)</uri>
```
> [!NOTE]
> The request message shows how to update the link to the first partner in the partnership, denoted by the **PartnerA** property. You can use a similar message to update the link with the second partner, using the **PartnerB** entity property.

## <a name="BKMK_DeletePartnership"></a>Delete a Partnership
You can delete a partnership using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partnerships(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/Partnerships(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreateLinkWithPartner"></a>Link Partners with Partnerships
In [Create a Partnership](/Topic/Partnership.md#BKMK_CreatePartnership) section, we saw how to create a link between a partnership and a partner while creating a partnership. In this section, we see how to create a link in the opposite direction, that is, from a partner to a partnership. To create the link, the URI of the partnership must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/PartnershipsAsA <br /> <br />or <br /> <br />[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/PartnershipsAsB <br /> <br />*Partner(id)* denotes the ID of the partner that links to the partnership <br /> <br />|HTTP/1.1 <br /> <br />|
> [!NOTE]
> There must always be two partners in a partnership, which means there must be two navigation properties on the Partner entity representing the two partners in the partnership. These properties are **PartnershipsAsA** and **PartnershipsAsB**. To create a partnership, you must create a link from one partner to partnership using the **PartnershipsAsA** property, and from the other partner to the same partnership entity using the **PartnershipsAsB** property. In both the cases, you must pass the URI of the partnership entity in the request body.
> 
> The following sample request message shows how to create a link between a partner and partnership using the **PartnershipsAsA** property.

### Sample Request

```
POST bts_svc_tpm_metadata/Partners(3)/$links/PartnershipsAsA HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 211
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/Partnerships(1)</uri>
```

## <a name="BKMK_DeletePartnershipsLink"></a>Delete Link between Partners and Partnerships
You can delete a link between partner and partnerships by using the HTTP DELETE method. To completely delete the links between two partners and a partnership, you must do the following:

- Delete the link between the first partner and partnership

- Delete the link between the second partner and partnership

- Delete the partnership

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/PartnershipsAsA(*id*) <br /> <br />or <br /> <br />[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/PartnershipsAsB(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
The following sample request deletes the link between the first partner and partnership, represented using the PartnershipsAsA navigation property. You can use a similar request to delete the link between the second partner and partnership. You should then delete the partnership entity as shown in [Delete a Partnership](/Topic/Partnership.md#BKMK_DeletePartnership) section.

```
DELETE bts_svc_tpm_metadata/Partners(1)/$links/PartnershipsAsA(1) HTTP/1.1
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

