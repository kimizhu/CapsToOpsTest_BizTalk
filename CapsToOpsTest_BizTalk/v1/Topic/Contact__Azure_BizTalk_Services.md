---
description: na
keywords: na
pagetitle: Contact| Azure BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb753ed4-8d8d-4bd1-ad4f-6922343caa0f
---
# Contact| Azure BizTalk Services
A `Contact` entity provides the contact information specific to a partner, a business profile, or an agreement.

- [Contact Entity Properties](/Topic/Contact__Azure_BizTalk_Services.md#BKMK_ContactProperties)

- [Create a Contact](/Topic/Contact__Azure_BizTalk_Services.md#BKMK_CreateContact)

- [List Contacts](/Topic/Contact__Azure_BizTalk_Services.md#BKMK_ListProfiles)

- [Update a Contact](/Topic/Contact__Azure_BizTalk_Services.md#BKMK_UpdateProfile)

- [Delete a Contact](/Topic/Contact__Azure_BizTalk_Services.md#BKMK_DeleteProfile)

- [Link Other Entities with Contacts](/Topic/Contact__Azure_BizTalk_Services.md#BKMK_CreatePartnerLink)

- [Delete Link between Other Entities and Contacts](/Topic/Contact__Azure_BizTalk_Services.md#BKMK_DeletePartnerLink)

## <a name="BKMK_ContactProperties"></a>Contact Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the contact. This value is auto-generated. <br /> <br />|
|Agreement <br /> <br />|Agreement <br /> <br />|A navigation property that references the agreement to which the contact details apply. <br /> <br />|
|BusinessProfile <br /> <br />|BusinessProfile <br /> <br />|**Required**. A navigation property that references the business profile to which the contact details apply. <br /> <br />|
|Partner <br /> <br />|Partner <br /> <br />|A navigation property that references the partner to which the contact details apply <br /> <br />|
|AddressLine1 <br /> <br />|String <br /> <br />|Specifies the address. This must not be more than 256 characters. <br /> <br />|
|AddressLine2 <br /> <br />|String <br /> <br />|Specifies the address. This must not be more than 256 characters. <br /> <br />|
|City <br /> <br />|String <br /> <br />|Specifies the city. This must not be more than 512 characters. <br /> <br />|
|Country <br /> <br />|String <br /> <br />|Specifies the country or region. This must not be more than 256 characters. <br /> <br />|
|EmailId <br /> <br />|String <br /> <br />|Specifies the e-mail ID. This must not be more than 256 characters. <br /> <br />|
|FirstName <br /> <br />|String <br /> <br />|Specifies the first name. This must not be more than 256 characters. <br /> <br />|
|LastName <br /> <br />|String <br /> <br />|Specifies the last name. This must not be more than 256 characters. <br /> <br />|
|Phone <br /> <br />|String <br /> <br />|Specifies the phone contact details. This must not be more than 256 characters. <br /> <br />|
|PostalCode <br /> <br />|String <br /> <br />|Specifies the postal code. This must not be more than 16 characters. <br /> <br />|
|State <br /> <br />|String <br /> <br />|Specifies the state. This must not be more than 256 characters. <br /> <br />|
|WebsiteURL <br /> <br />|String <br /> <br />|Specifies the website URL. This must not be more than 256 characters. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

### Considerations
A `Contact` entity must be associated with either a `Partner`, a `BusinessProfile`, or an `Agreement` entity.

## <a name="BKMK_CreateContact"></a>Create a Contact
You can create a contact using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Contacts <br /> <br />|HTTP/1.1 <br /> <br />|
> [!NOTE]
> You cannot create a contact without linking it to a partner, a business profile, or an agreement. In the following sample request, a contact is linked to a business profile using the **&lt;link&gt;** element of the request body.

### Sample Request

```
POST bts_svc_tpm_metadata/Contacts HTTP/1.1
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
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.Contact" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/BusinessProfile" type="application/atom+xml;type=entry" title="BusinessProfile" href="bts_svc_tpm_metadata/BusinessProfiles(1)" />
  <id />
  <title />
  <updated>2013-02-01T18:28:40Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:City>Redmond</d:City>
      <d:FirstName>John</d:FirstName>
      <d:LastName>Smith</d:LastName>
       <d:State>WA</d:State>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListProfiles"></a>List Contacts
You can list contacts using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Contacts <br /> <br />This returns all the business profiles <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Contacts(*id*) <br /> <br />This returns information about the contacts with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the contacts**

```
GET bts_svc_tpm_metadata/Contacts HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/json
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific contact**

```
GET bts_svc_tpm_metadata/Contacts(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/json
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateProfile"></a>Update a Contact
You can update a contact using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Contacts <br /> <br />(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/Contacts(id) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/atom+xml
If-Match: W/"X'00000000000010BF'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 790
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/Contacts(2)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.Contact" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-01T19:18:10Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:FirstName>Jeff</d:FirstName>
      <d:LastName>Chia</d:LastName>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteProfile"></a>Delete a Contact
You can delete a business profile using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Contacts(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/Contacts(1) HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
If-Match: W/"X'00000000000010C0'"
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_CreatePartnerLink"></a>Link Other Entities with Contacts
In [Create a Contact](/Topic/Contact__Azure_BizTalk_Services.md#BKMK_CreateContact) section, we saw how to create a link between a contact and business profile while creating a contact. In this section, we see how to create a link in the opposite direction, that is, from a another entity (for example, partner) to a contact. To create the link, the URI of the contact entity must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/Contacts <br /> <br />*Partner(id)* denotes the ID of the partner that links to the contact <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/Partners(1)/$links/Contacts HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
x-ms-version: 1.0
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 208
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/Contacts(2)</uri>
```

## <a name="BKMK_DeletePartnerLink"></a>Delete Link between Other Entities and Contacts
You can delete a link between other entities and contacts by using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/Partners(*id*)/$links/Contacts(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/Partners(1)/$links/Contacts(2) HTTP/1.1
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

