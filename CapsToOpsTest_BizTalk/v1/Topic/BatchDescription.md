---
description: na
keywords: na
pagetitle: BatchDescription
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6801ba4d-280c-41e0-b178-c7c68c3636bb
---
# BatchDescription
A `BatchDescription` entity set captures batch configuration for each send-side one-way agreement.

- [BatchDescription Entity Properties](/Topic/BatchDescription.md#BKMK_EntityProperties)

- [Create a Batch Description](/Topic/BatchDescription.md#BKMK_CreateBatchDesc)

- [List BatchDescriptions](/Topic/BatchDescription.md#BKMK_ListBatchDesc)

- [Update a BatchDescription](/Topic/BatchDescription.md#BKMK_UpdateBatchDesc)

- [Delete a Batch Description](/Topic/BatchDescription.md#BKMK_DeleteBatchDesc)

- [Link OnewayAgreements with BatchDescriptions](/Topic/BatchDescription.md#BKMK_CreateLink)

- [Delete Link between OnewayAgreements and BatchDescriptions](/Topic/BatchDescription.md#BKMK_DeletePartnerLink)

## <a name="BKMK_EntityProperties"></a>BatchDescription Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|ID <br /> <br />|Int <br /> <br />|Specifies a unique ID for the batch. This value is auto-generated. <br /> <br />|
|Name <br /> <br />|String <br /> <br />|**Required**. Specifies a unique name for the batch. This must not be more than 256 characters. <br /> <br />|
|Description <br /> <br />|String <br /> <br />|Specifies a description for the batch. This must not be more than 256 characters. <br /> <br />|
|CriteriaType <br /> <br />|String <br /> <br />|**Required**. &lt;Pending meeting&gt; <br /> <br />|
|FilterExpression <br /> <br />|String <br /> <br />|**Required**. Specifies a valid SQL92 filter expression. This must not be more than 1024 characters. <br /> <br />|
|FirstRelease <br /> <br />|DateTime <br /> <br />|**Required** if the **ReleaseCriteriaType** is set to **Schedule**. This specifies the time when the first batch is released. <br /> <br />|
|InterchangeSize <br /> <br />|Long <br /> <br />|**Required** if the **ReleaseCriteriaType** is set to **Size**. This specifies the total size of the batch to wait for before releasing the batch. <br /> <br />|
|MessageCount <br /> <br />|Int <br /> <br />|**Required** if the **ReleaseCriteriaType** is set to **Count**. This specifies the count of the message to wait for before releasing the batch. <br /> <br />|
|MessageScope <br /> <br />|Short <br /> <br />|**Required** if the **ReleaseCriteriaType** is set to **Count**. The possible value is 1, which indicates that each interchange is treated as a separate message. <br /> <br />|
|OnewayAgreement <br /> <br />|OnewayAgreement <br /> <br />|**Required**. A navigation property that references the one-way send-side agreement with which the batch setting is associated. <br /> <br />|
|ProtocolName <br /> <br />|String <br /> <br />|**Required**. Specifies the protocol for the agreement with which batch setting is associated. <br /> <br />|
|RecurrencePeriodInSeconds <br /> <br />|Long <br /> <br />|**Required** if **ReleaseCriteriaType** is set to **Schedule**. <br /> <br />|
|RecurrenceType <br /> <br />|Short <br /> <br />|**Required** if the ReleaseCriteriaType is set to Schedule. This property specifies whether the frequency of recurrence is based on minutes, hours, etc. The possible values are: <br /> <br /><ul><li>None = 0 </li><li>MinutesBased </li> </ul>|
|TimeoutInSeconds <br /> <br />|Long <br /> <br />|Required if the **ReleaseCriteriaType** is set to **Timeout**. This property specifies the timeout (in seconds) at which a batch is triggered, irrespective of whether any other criterion is met or not. <br /> <br />|
|DaysOfWeek <br /> <br />|Int <br /> <br />|Required if the **ReleaseCriteriaType** is set to **Schedule**. This specifies the day of the week when the batch is released. The possible values are Monday=1 to Sunday=7. <br /> <br />|
|StartDateInternal <br /> <br />|DateTime <br /> <br />|Specifies the start date for the batch. <br /> <br />|
|EndDateInternal <br /> <br />|DateTime <br /> <br />|Specifies the end date for the batch <br /> <br />|
|TerminationCount <br /> <br />|Int <br /> <br />||
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## <a name="BKMK_CreateBatchDesc"></a>Create a Batch Description
You can create a batch description using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BatchDescriptions <br /> <br />|HTTP/1.1 <br /> <br />|
> [!NOTE]
> You cannot create a business profile without linking it to a partner. In the following sample request, a business profile is linked to a partner using the **&lt;link&gt;** element of the request body.

> [!NOTE]
> After you create a new batch using the TPM OM API, you must redeploy the agreement using the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

### Sample Request
The following sample request message shows how to create a batch description and simultaneously create a link with a OnewayAgreement entity using the **&lt;link&gt;** element in the request body.

```
POST bts_svc_tpm_metadata/BatchDescriptions HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 1753
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.BatchDescription" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/OnewayAgreement" type="application/atom+xml;type=entry" title="OnewayAgreement" href="bts_svc_tpm_metadata/OnewayAgreements(90)" />
  <id />
  <title />
  <updated>2013-02-08T06:51:24Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:CriteriaType m:type="Edm.Int16">0</d:CriteriaType>
      <d:DaysOfWeek m:type="Edm.Int32" m:null="true" />
      <d:Description m:null="true" />
      <d:EndDateInternal m:type="Edm.DateTime">0001-01-01T00:00:00</d:EndDateInternal>
      <d:FilterExpression>1=1</d:FilterExpression>
      <d:FirstRelease m:type="Edm.DateTime">2013-02-07T22:51:24.6239514-08:00</d:FirstRelease>
      <d:Id m:type="Edm.Int32">0</d:Id>
      <d:InterchangeSize m:type="Edm.Int64" m:null="true" />
      <d:MessageCount m:type="Edm.Int32" m:null="true" />
      <d:MessageScope m:type="Edm.Int16" m:null="true" />
      <d:Name>NewBatch</d:Name>
      <d:ProtocolName>X12</d:ProtocolName>
      <d:RecurrencePeriodInSeconds m:type="Edm.Int64" m:null="true" />
      <d:RecurrenceType m:type="Edm.Int16" m:null="true" />
      <d:StartDateInternal m:type="Edm.DateTime">0001-01-01T00:00:00</d:StartDateInternal>
      <d:TerminationCount m:type="Edm.Int32" m:null="true" />
      <d:TimeoutInSeconds m:type="Edm.Int64" m:null="true" />
      <d:Version m:type="Edm.Binary">AA==</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListBatchDesc"></a>List BatchDescriptions
You can list batch descriptions using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BatchDescriptions <br /> <br />This returns all the batch descriptions <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BatchDescriptions(*id*) <br /> <br />This returns information about the batch description with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the batch descriptions**

```
GET bts_svc_tpm_metadata/BatchDescriptions HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific batch description**

```
GET bts_svc_tpm_metadata/BatchDescriptions(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateBatchDesc"></a>Update a BatchDescription
You can update a batch description using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BatchDescriptions(id) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/BatchDescriptions(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
If-Match: W/"X'0000000000000A59'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 1598
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/BatchDescriptions(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.BatchDescription" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-08T07:29:29Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      <d:CriteriaType m:type="Edm.Int16">0</d:CriteriaType>
      <d:DaysOfWeek m:type="Edm.Int32" m:null="true" />
      <d:Description m:null="true" />
      <d:EndDateInternal m:type="Edm.DateTime">0001-01-01T00:00:00</d:EndDateInternal>
      <d:FilterExpression>1=1</d:FilterExpression>
      <d:FirstRelease m:type="Edm.DateTime">2013-02-07T17:26:48.7885402</d:FirstRelease>
      <d:Id m:type="Edm.Int32">1</d:Id>
      <d:InterchangeSize m:type="Edm.Int64" m:null="true" />
      <d:MessageCount m:type="Edm.Int32" m:null="true" />
      <d:MessageScope m:type="Edm.Int16" m:null="true" />
      <d:Name>UpdatedBatch</d:Name>
      <d:ProtocolName>X12</d:ProtocolName>
      <d:RecurrencePeriodInSeconds m:type="Edm.Int64" m:null="true" />
      <d:RecurrenceType m:type="Edm.Int16" m:null="true" />
      <d:StartDateInternal m:type="Edm.DateTime">0001-01-01T00:00:00</d:StartDateInternal>
      <d:TerminationCount m:type="Edm.Int32" m:null="true" />
      <d:TimeoutInSeconds m:type="Edm.Int64" m:null="true" />
      <d:Version m:type="Edm.Binary">AAAAAAAAClk=</d:Version>
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteBatchDesc"></a>Delete a Batch Description
You can delete a batch description using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/BatchDescriptions(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/BatchDescriptions(1) HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
If-Match: W/"X'0000000000000A5F'"
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreateLink"></a>Link OnewayAgreements with BatchDescriptions
In [Create a Batch Description](/Topic/BatchDescription.md#BKMK_CreateBatchDesc) section, we saw how to create a link between a BatchDescription and a OnewayAgreement while creating a BatchDescription. In this section, we see how to create a link in the opposite direction, that is, from a OnewayAgreement to a BatchDescription. To create the link, the URI of the BatchDescription must be included in the request body.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/OnewayAgreements(*id*)/$links/BatchDescriptions <br /> <br />*OnewayAgreements(id)* denotes the ID of the one-way agreement that links to the batch description. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/OnewayAgreements(1)/$links/BatchDescriptions HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 216
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">bts_svc_tpm_metadata/BatchDescriptions(1)</uri>
```

## <a name="BKMK_DeletePartnerLink"></a>Delete Link between OnewayAgreements and BatchDescriptions
You can delete a link between OnewayAgreements and BatchDescriptions by using the HTTP DELETE method.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/OnewayAgreements(*id*)/$links/BatchDescriptions(*id*) <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/OnewayAgreements(1)/$links/BatchDescriptions(1) HTTP/1.1
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

