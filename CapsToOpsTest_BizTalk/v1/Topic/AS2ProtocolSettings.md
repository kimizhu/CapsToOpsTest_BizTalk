---
description: na
keywords: na
pagetitle: AS2ProtocolSettings
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef64d72e-b832-456c-a7ab-af15c25b2b61
---
# AS2ProtocolSettings
An `AS2ProtocolSettings` entity inherits the `ProtocolSettings` entity and provides the AS2 protocol information.

- [AS2ProtocolSettings Entity Properties](/Topic/AS2ProtocolSettings.md#BKMK_EntityProps)

- [Create an AS2ProtocolSettings](/Topic/AS2ProtocolSettings.md#BKMK_CreateAS2)

- [List AS2 Protocol Settings](/Topic/AS2ProtocolSettings.md#BKMK_ListAS2Setting)

- [Update an AS2 Protocol Setting](/Topic/AS2ProtocolSettings.md#BKMK_UpdateAS2)

- [Delete an AS2 Protocol Setting](/Topic/AS2ProtocolSettings.md#BKMK_DeleteAS2)

## <a name="BKMK_EntityProps"></a>AS2ProtocolSettings Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|AckHttpExpect100Continue <br /> <br />|Bool <br /> <br />|Specifies that the posted data is not included in the initial HTTP request, and waits for the server to request the content. <br /> <br />|
|AckIgnoreCertificateNameMismatch <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the SSL connection is accepted even if the server name does not match the server name that the SSL certificate was generated for. <br /> <br />|
|AckKeepHttpConnectionAlive <br /> <br />|Bool <br /> <br />|Specifies that an HTTP connection is kept alive even after a request and response cycle is completed. <br /> <br />|
|AckUnfoldHttpHeaders <br /> <br />|Bool <br /> <br />|Specifies whether the HTTP content-type header is unfolded into a single line. <br /> <br />|
|AutogenerateFileName <br /> <br />|Bool <br /> <br />|Specifies whether the bridge generates a filename <br /> <br />|
|CheckCertificateRevocationListOnReceive <br /> <br />|Bool <br /> <br />|Specifies whether the certificate to be used in decrypting a received message is included in the Certificate Revocation List. <br /> <br />|
|CheckCertificateRevocationListOnSend <br /> <br />|Bool <br /> <br />|Specifies whether the certificate to be used in signing an outgoing message is included in the Certificate Revocation List. <br /> <br />|
|CheckDuplicateInterchangeControlNumber <br /> <br />|Bool <br /> <br />|Specifies whether the bridge checks for duplicate interchange control numbers in the received message. <br /> <br />|
|DispositionNotificationTo <br /> <br />|String <br /> <br />|Specifies whether the party sending the MDN, signs the MDN, if the generation of MDN is enabled by the Disposition-Notification-To header of the AS2 message. <br /> <br />|
|EnableNRRForInboundDecodedMessages <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether inbound decoded AS2 messages are stored in the non-repudiation database. <br /> <br />|
|EnableNRRForInboundEncodedMessages <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether inbound encoded AS2 messages are stored in the non-repudiation database. <br /> <br />|
|EnableNRRForInboundMDN <br /> <br />|Bool <br /> <br />|Specifies whether the inbound MDN is stored in the non-repudiation database. <br /> <br />|
|EnableNRRForOutboundDecodedMessages <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether outbound decoded AS2 messages are stored in the non-repudiation database. <br /> <br />|
|EnableNRRForOutboundEncodedMessages <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether outbound encoded AS2 messages are stored in the non-repudiation database. <br /> <br />|
|EnableNRRForOutboundMDN <br /> <br />|Bool <br /> <br />|Specifies whether the outbound MDN is stored in the non-repudiation database. <br /> <br />|
|EncryptionAlgorithm <br /> <br />|Short <br /> <br />|**Required**. Specifies the encryption algorithm. The valid values are: <br /> <br /><ul><li>**0** – For DES3 </li><li>**1** – For RC2 </li> </ul>|
|EncryptionCertificateId <br /> <br />|Int <br /> <br />|Specifies the encryption certificate ID. <br /> <br />|
|EncryptionCertificateThumbprint <br /> <br />|String <br /> <br />|Specifies the thumbprint of the certificate used for encryption. This value must not exceed 128 characters. <br /> <br />|
|FileNameTemplate <br /> <br />|String <br /> <br />|Specifies a string value for filename. <br /> <br />|
|HttpExpect100Continue <br /> <br />|Bool <br /> <br />|Specifies that the posted data is not included in the initial HTTP request, and waits for the server to request the content. <br /> <br />|
|HttpRetryTimeoutTicks <br /> <br />|Long <br /> <br />|- <br /> <br />|
|IgnoreCertificateNameMismatch <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the SSL connection is accepted even if the server name does not match the server name that the SSL certificate was generated for. <br /> <br />|
|InterchangeDuplicatesValidity <br /> <br />|Short <br /> <br />|- <br /> <br />|
|KeepHttpConnectionAlive <br /> <br />|Bool <br /> <br />|Specifies that an HTTP connection is kept alive even after a request and response cycle is completed. <br /> <br />|
|MaximumHttpRetryAttempts <br /> <br />|Int <br /> <br />|Specifies the maximum amount of time to attempt retries using HTTP. <br /> <br />|
|MaxResendAttempts <br /> <br />|Int <br /> <br />|Specifies the maximum number of resend attempts to be made <br /> <br />|
|MicHashingAlgorithm <br /> <br />|Short <br /> <br />|**Required**. Specifies the MIC algorithm. <br /> <br />|
|MDNText <br /> <br />|String <br /> <br />|Specifies a text that the sending partner adds to the MDN messages (under the Content-Description field). <br /> <br />|
|MessageCompressed <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the AS2 message is compressed. <br /> <br />|
|MessageContentType <br /> <br />|String <br /> <br />|**Required**. Specifies the default content-type of the message. <br /> <br />|
|MessageEncrypted <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the AS2 message is encrypted. <br /> <br />|
|MessageSigned <br /> <br />|Bool <br /> <br />|Required. Specifies whether the AS2 message is signed. <br /> <br />|
|MinimumHttpRetryTicks <br /> <br />|Long <br /> <br />|Specifies the minimum amount of time to attempt retries using HTTP. <br /> <br />|
|SendMDNAsynchronously <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether an MDN is sent asynchronously. <br /> <br />|
|NeedMdn <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a trading partner must generate an MDN in response to an AS2 message. <br /> <br />|
|SignMdn <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the MDN must be signed using SHA1 or MD5. <br /> <br />|
|OverrideMessageProperties <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the message properties are overridden. <br /> <br />|
|ProtocolName <br /> <br />|String <br /> <br />|Specifies the protocol name. The valid value is **as2**. <br /> <br />|
|ReceiptDeliverUrl <br /> <br />|String <br /> <br />|Specifies the URL at which the receiving party must send the MDN. This must not be more than 256 characters. <br /> <br />|
|SigningCertificateId <br /> <br />|Int <br /> <br />|Specifies the ID of the signing certificate. <br /> <br />|
|SigningCertificateThumbprint <br /> <br />|String <br /> <br />|Specifies the thumbprint of the certificate used for signing. This value must not be greater than 128 characters. <br /> <br />|
|SignOutboundMdnIfOptional <br /> <br />|Bool <br /> <br />|**Required**. <br /> <br />|
|SuspendDuplicateMessage <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a duplicate AS2 message is suspended. <br /> <br />|
|SuspendMessageOnFileNameGenerationError <br /> <br />|Bool <br /> <br />|**Required**. <br /> <br />|
|TransmitFileNameInMimeHeader <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a file name is sent as part of a MIME header of an outbound AS2 message. <br /> <br />|
|UnfoldHttpHeaders <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the HTTP content-type header is unfolded into a single line. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## <a name="BKMK_CreateAS2"></a>Create an AS2ProtocolSettings
You can create an AS2 protocol settings entity using a POST HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/ProtocolSettings HTTP/1.1
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
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <id />
  <title />
  <updated>2013-02-13T18:46:57Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      ...
     [ Property names with their values ]
     ...
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListAS2Setting"></a>List AS2 Protocol Settings
You can list the AS2 protocol settings using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings/Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings <br /> <br />This returns all the protocol settings entities <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(*id*)/Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings <br /> <br />This returns information about the protocol setting with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the protocol settings**

```
GET bts_svc_tpm_metadata/ProtocolSettings/Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```
**Retrieve information about a specific protocol setting**

```
GET bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateAS2"></a>Update an AS2 Protocol Setting
You can update an AS2 protocol setting using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(id)/ Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 4724
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/ProtocolSettings(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-13T19:05:16Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      ...
      [ Updated Properties with their values ]
      ...
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteAS2"></a>Delete an AS2 Protocol Setting
You can delete an AS2 protocol setting using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(*id*)/Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.AS2ProtocolSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

