---
description: na
keywords: na
pagetitle: X12ProtocolSettings
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 678eb2b4-1734-4aca-a3e0-2022a7bc7dfa
---
# X12ProtocolSettings
An `X12ProtocolSettings` entity inherits the `ProtocolSettings` entity and provides the X12 protocol information.

- [X12ProtocolSettings Entity Properties](/Topic/X12ProtocolSettings.md#BKMK_X12EntityProperties)

- [Create an X12ProtocolSettings](/Topic/X12ProtocolSettings.md#BKMK_CreateX12)

- [List X12 Protocol Settings](/Topic/X12ProtocolSettings.md#BKMK_ListX12Setting)

- [Update a Protocol Setting](/Topic/X12ProtocolSettings.md#BKMK_UpdateX12)

- [Delete an X12 Protocol Setting](/Topic/X12ProtocolSettings.md#BKMK_DeleteX12Setting)

- [Link X12ProtocolSettings with Other Entities](/Topic/X12ProtocolSettings.md#BKMK_CreateLink)

- [Delete Link between X12ProtocolSettings and Other Entities](/Topic/X12ProtocolSettings.md#BKMK_DeleteSchemaRefLink)

## <a name="BKMK_X12EntityProperties"></a>X12ProtocolSettings Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|Id <br /> <br />|Int <br /> <br />|Specifies a unique ID for the X12 protocol settings. This value is auto-generated. <br /> <br />|
|AcknowledgementControlNumberLowerBound <br /> <br />|Int <br /> <br />|**Required**. Specifies a numeric value for the lower bounds for the acknowledgement control number. The possible values are between 1 and 999999999. <br /> <br />|
|AcknowledgementControlNumberPrefix <br /> <br />|String <br /> <br />|Specifies a prefix for the acknowledgement control number. This value can be alpha-numeric and must not be more than 9 characters. <br /> <br />|
|AcknowledgementControlNumberSuffix <br /> <br />|String <br /> <br />|Specifies a suffix for the acknowledgement control number. This value can be alpha-numeric and must not be more than 9 characters. <br /> <br />|
|AcknowledgementControlNumberUpperBound <br /> <br />|Int <br /> <br />|**Required**. Specifies a numeric value for the upper bounds for the acknowledgement control number. The possible values are between 1 and 999999999. <br /> <br />|
|AcknowledgementControlNumberRollover <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the control number is reset to the lower limit once the maximum value is exceeded. <br /> <br />|
|AllowLeadingAndTrailingSpacesAndZeroes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the EDI interchange fails validation if a data element in the interchange does not conform to its length requirement because of leading (or trailing) zeroes or trailing spaces, but does conform to its length requirement when they are removed. <br /> <br />|
|AuthorizationQualifier <br /> <br />|String <br /> <br />|**Required**. Specifies the authorization qualifier and must not be more than 2 characters long. The possible values are: <br /> <br /><ul><li>**00** – for no authorization </li><li>**01** – for UCSCommunicationsId </li><li>**02** – for EDXCommunicationsId </li><li>**03** – for AdditionalDataId </li><li>**04** – for RailCommunicationId </li><li>**05** – for DoDCommunicationsId </li><li>**06** – for USFederalGovernmentCommunicationsId </li><li>**07** – for TruckCommunicationsId </li><li>**08** – for OceanCommunicationsId </li> </ul>|
|AuthorizationValue <br /> <br />|String <br /> <br />|You must specify this value if you set **AuthorizationQualifier** to any value other than **00**. This field must not be more than 10 characters. <br /> <br />|
|BatchFunctionalAck <br /> <br />|Bool <br /> <br />|**Required**. Set this to true to send functional acknowledgements in batches. If set to false, each functional acknowledgement is sent separately. <br /> <br />|
|BatchTechnicalAck <br /> <br />|Bool <br /> <br />|**Required**. Set this to true to send technical acknowledgements in batches. If set to false, each technical acknowledgement is sent separately. <br /> <br />|
|CharacterSet <br /> <br />|Short <br /> <br />|**Required**. Specifies the character set. The valid values are **0**, **1**, or **2**. <br /> <br />|
|CheckDuplicateGroupControlNumber <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether interchanges with duplicate group control numbers (GS06) are processed. <br /> <br />|
|CheckDuplicateInterchangeControlNumber <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether interchanges with duplicate interchange control numbers (ISA13) are processed. This checks the interchange control number for the received interchange with the interchange control number of an earlier message. If a match occurs, the bridge processes the interchange based on the value of this property. <br /> <br />|
|CheckDuplicateTransactionSetControlNumber <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether interchanges with duplicate transaction sets (ST02) are processed. <br /> <br />|
|ComponentSeparator <br /> <br />|Int <br /> <br />|**Required**. Specifies the component separator used by the bridge to identify the different components in the message. This value must not be an empty space, an alphabet, or a numeric character. <br /> <br />|
|ControlStandardsId <br /> <br />|Int <br /> <br />|**Required**. Specifies the control standards ID. The possible value is **U**. However, if **UseControlStandardsIdAsRepSep** is set to true, the value of **ControlStandardsId** can be set to the repetition character. Also, the repetition character must not be a space, an alphabet, or a numberic character. <br /> <br />|
|ControlVersionNumber <br /> <br />|String <br /> <br />|**Required**. Specifies the version of the X12 standard to be used for generating an outgoing interchange. This must not exceed 5 characters, for example, **00401**. <br /> <br />|
|ConvertImpliedDecimal <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether an EDI number, specified with the format Nn, is converted base-10 numeric value in the intermediate XML file. <br /> <br />|
|CreateEmptyXmlTagsForTrailingSeparators <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether empty XML tags are included for trailing separators. <br /> <br />|
|DataElementSeparator <br /> <br />|Int <br /> <br />|**Required**. Specifies a single character that the bridge uses to separate composite data elements consisting of two or more simple data elements. <br /> <br />|
|DelimiterOverrides <br /> <br />|DataServiceCollection&lt;X12DelimiterOverride&gt; <br /> <br />|A navigation property that references the delimiter overrides associated with an X12 message. <br /> <br />|
|EnableDefaultGroupHeaders <br /> <br />|Bool <br /> <br />|Specifies whether default group headers are included or not. <br /> <br />|
|EnvelopeOverrides <br /> <br />|DataServiceCollection&lt;X12EnvelopeOverride&gt; <br /> <br />|A navigation property that references the envelop overrides associated with an X12 message. <br /> <br />|
|FunctionalGroupId <br /> <br />|String <br /> <br />||
|GenerateLoopForValidMessagesInAck <br /> <br />|Bool <br /> <br />|Required. Specifies whether the AK2 loops are generated in the 997 acknowledgements for accepted transaction sets. <br /> <br />|
|GroupControlNumberLowerBound <br /> <br />|Int <br /> <br />|Specifies a numeric value for the lower bounds for the group control number. The possible values are between 1 and 999999999. <br /> <br />|
|GroupControlNumberRollover <br /> <br />|Bool <br /> <br />|Specifies whether the group control number is reset to the lower limit once the maximum value is exceeded. <br /> <br />|
|GroupControlNumberUpperBound <br /> <br />|Int <br /> <br />|Specifies a numeric value for the upper bounds for the group control number. The possible values are between 1 and 999999999. This value must be greater than or equal to the value for **GroupControlNumberLowerBound**. <br /> <br />|
|GroupDateFormat <br /> <br />|String <br /> <br />|**Required**. Specifies the group date format. The valid values are **CCYYMMDD** or **YYMMDD**. <br /> <br />|
|GroupHeaderVersion <br /> <br />|String <br /> <br />|Specifies the group header version. The valid value is **00401**. Also, the value must not exceed 12 characters. <br /> <br />|
|GroupResponsibleAgencyCode <br /> <br />|Short <br /> <br />|**Required**. Specifies the responsible agency code (GS07) for the group. The valid values are: <br /> <br /><ul><li>**84** – for TransportationDataCoordingationCommittee </li><li>**88** – for AccreditedStandardsCommittee </li> </ul>|
|GroupTimeFormat <br /> <br />|Short <br /> <br />|**Required**. Specifies the group time format. The valid values are **HHMM**, **HHMMSS**, **HHMMSSdd**, **HHMMSSd**. <br /> <br />|
|InterchangeControlNumberLowerBound <br /> <br />|Int <br /> <br />|**Required**. Specifies a numeric value for the lower bounds for the interchange control number. The possible values are between 1 and 999999999. <br /> <br />|
|InterchangeControlNumberRollover <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the interchange control number is reset to the lower limit once the maximum value is exceeded. <br /> <br />|
|InterchangeControlNumberUpperBound <br /> <br />|Int <br /> <br />|**Required**. Specifies a numeric value for the upper bounds for the interchange control number. The possible values are between 1 and 999999999. This value must be greater than or equal to the value for **InterchangeControlNumberLowerBound**. <br /> <br />|
|InterchangeDuplicatesValidity <br /> <br />|Short <br /> <br />|**Required**. You must set this property if **CheckDuplicateInterchangeControlNumber** property is set to **True**. If set, this property can only take values greater than 0. <br /> <br />|
|MaskSecurityInfo <br /> <br />|Bool <br /> <br />|- <br /> <br />|
|MessageFilterType <br /> <br />|Short <br /> <br />|Specifies the type of message filter. The valid values are **Include** and **Exclude**. <br /> <br />|
|NeedFunctionalAck <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a functional acknowledgement (997) must be returned to the interchange sender. <br /> <br />|
|NeedTechnicalAck <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a technical acknowledgement (TA1) must be returned to the interchange sender. <br /> <br />|
|PreserveInterchange <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the bridge preserves an EDI interchange. <br /> <br />|
|ProtocolName <br /> <br />|String <br /> <br />|**Required**. Specifies the protocol name. The only valid value for this property is **X12**. <br /> <br />|
|ReceiverApplicationId <br /> <br />|String <br /> <br />|Specifies the receiver application ID. This value must not exceed 15 characters. <br /> <br />|
|ReplaceChar <br /> <br />|Int <br /> <br />|You must set this property if **ReplaceSeparatorsInPayload** property is set to **True**. <br /> <br />|
|ReplaceSeparatorsInPayload <br /> <br />|Bool <br /> <br />|If set to True, all instances of the separator characters in the payload data are replaced with the character specified for the property **ReplaceChar**. <br /> <br />|
|RouteAckToSendPipeline <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the acknowledgement must be returned by a separate channel. <br /> <br />|
|SchemaReferences <br /> <br />|DataServiceCollection&lt;X12SchemaReference&gt; <br /> <br />|A navigation property that references the schema used for the X12 protocol settings. <br /> <br />|
|SecurityQualifier <br /> <br />|String <br /> <br />|**Required**. Specifies the security qualifier (ISA13). This must not exceed 2 characters and the valid values are: <br /> <br /><ul><li>**00** – for no security </li><li>**01** – for password security </li><li>**03** – for backward compatible password </li> </ul>|
|SecurityValue <br /> <br />|String <br /> <br />|Specifies the security value (ISA4). This property must be set if the **SecurityQualifier** property is not set to **00**. This property must not exceed 10 characters. <br /> <br />|
|SegmentTerminator <br /> <br />|Int <br /> <br />|**Required**. Specifies a single character that the bridge uses to indicate the end of a segment. This value must not be a space, an alphabet, or a numeric character. <br /> <br />|
|SegmentTerminatorSuffix <br /> <br />|Short <br /> <br />|**Required**. Specifies the character that the bridge uses with the segment terminator. The valid values are: <br /> <br /><ul><li>**00** – for None </li><li>**01** – for CR </li><li>**02** – for LF </li><li>**03** – for CRLF </li> </ul>|
|SenderApplicationId <br /> <br />|String <br /> <br />|Specifies the sender application ID. This value must not be more than 15 characters. <br /> <br />|
|SuspendInterchangeOnError <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the entire message is suspended if one or more transaction sets in the interchange fail validation. <br /> <br />|
|TrailingSeparatorPolicy <br /> <br />|Short <br /> <br />|**Required**. Specifies how to process trailing separators. <br /> <br /><ul><li>Set this to **0** (for Not Allowed). If set to 0, trailing delimiters and separators are not allowed in an interchange received from the interchange sender. If the interchange contains trailing delimiters and separators, it will be declared invalid. </li><li>Set this to **1** (for Mandatory). If set to 1, the received interchange must contain trailing delimiters and separators. </li><li>Set this to **2** (for Optional). If set to 2, the bridge accepts interchanges with or without trailing delimiters and separators. </li> </ul>|
|TSApplyNewId <br /> <br />|Bool <br /> <br />|**Required**. - <br /> <br />|
|TSControlNumberLowerBound <br /> <br />|Int <br /> <br />|**Required**. Specifies a numeric value for the lower bounds for the transaction set control number. The possible values are between 1 and 999999999. <br /> <br />|
|TSControlNumberPrefix <br /> <br />|String <br /> <br />|Specifies a prefix for the transaction set control number. This value can be alpha-numeric and must not be more than 9 characters. <br /> <br />|
|TSControlNumberRollover <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the control number is reset to the lower limit once the maximum value is exceeded. <br /> <br />|
|TSControlNumberSuffix <br /> <br />|String <br /> <br />|Specifies a suffix for the transaction set control number. This value can be alpha-numeric and must not be more than 9 characters. <br /> <br />|
|TSControlNumberUpperBound <br /> <br />|Int <br /> <br />|**Required**. Specifies a numeric value for the upper bounds for the transaction set control number. The possible values are between 1 and 999999999. <br /> <br />|
|UsageIndicator <br /> <br />|Short <br /> <br />|**Required**. Specifies whether an interchange generated by the bridge is information, production data, or test data. The possible values are: <br /> <br /><ul><li>**0** – for Test data </li><li>**1** – for Information </li><li>**2** – for Production data </li> </ul>|
|UseControlStandardsIDAsRepSep <br /> <br />|Bool <br /> <br />|**Required**. If set to false, the value of ISA11 is used to specify a standard identifier instead of a repetition separator. <br /> <br />|
|UseDotAsDecimalIndicator <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a dot (.) is used as a decimal separator. <br /> <br />|
|ValidateCharacterSet <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the character set must be validated. <br /> <br />|
|ValidateEdiTypes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether EDI (data element) validation is enabled on the interchange receiver. <br /> <br />|
|ValidateExtended <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether extended validation (XSD) is enabled on the interchange receiver. <br /> <br />|
|ValidationOverrides <br /> <br />|DataServiceCollection&lt;X12ValidationOverride&gt; <br /> <br />|A navigation property that references X12 validation overrides associated with the instance of X12 protocol settings. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## <a name="BKMK_CreateX12"></a>Create an X12ProtocolSettings
You can create an X12 protocol settings entity using a POST HTTP request.

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
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <id />
  <title />
  <updated>2013-02-05T19:38:38Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      ...
      [Property names with their values]
      ...
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_ListX12Setting"></a>List X12 Protocol Settings
You can list the X12 protocol settings using a GET HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings <br /> <br />This returns all the protocol settings entities <br /> <br />|HTTP/1.1 <br /> <br />|
|GET <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(*id*)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings <br /> <br />This returns information about the protocol setting with the specified ID. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request
**Retrieve all the protocol settings**

```
GET bts_svc_tpm_metadata/ProtocolSettings/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings HTTP/1.1
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
GET bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
```

## <a name="BKMK_UpdateX12"></a>Update a Protocol Setting
You can update an X12 protocol setting using a MERGE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|MERGE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(id)/ Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
MERGE bts_svc_tpm_metadataProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/atom+xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 5446
Expect: 100-continue

<entry xmlns="http://www.w3.org/2005/Atom" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  <id>bts_svc_tpm_metadata/ProtocolSettings(1)</id>
  <category term="Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <title />
  <updated>2013-02-05T23:59:14Z</updated>
  <author>
    <name />
  </author>
  <content type="application/xml">
    <m:properties>
      ...
      [Upddated properties with their values]
      ...
    </m:properties>
  </content>
</entry>
```

## <a name="BKMK_DeleteX12Setting"></a>Delete an X12 Protocol Setting
You can delete an X12 protocol setting using a DELETE HTTP request.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|DELETE <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ProtocolSettings(*id*)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
DELETE bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings HTTP/1.1
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 0
```

## <a name="BKMK_CreateLink"></a>Link X12ProtocolSettings with Other Entities
You can link an X12 protocol setting entity with other entities using the POST HTTP method. To create the link, the URI of the entity you are linking to must be included in the request body. In this section, we show how to create a link between X12ProtocolSetting and X12SchemaReference.

|Method <br /> <br />|Request URI <br /> <br />|HTTP Version <br /> <br />|
|----------|---------------|----------------|
|POST <br /> <br />|[!INCLUDE[bts_svc_tpm_metadata](/Token/bts_svc_tpm_metadata_md.md)]/ ProtocolSettings(id)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/SchemaReferences <br /> <br />*ProtocolSettings(id)* denotes the ID of the protocol setting that links to the X12 schema reference. <br /> <br />|HTTP/1.1 <br /> <br />|

### Sample Request

```
POST bts_svc_tpm_metadata/ProtocolSettings(1)/Microsoft.ApplicationServer.Integration.PartnerManagement.X12ProtocolSettings/$links/SchemaReferences HTTP/1.1
User-Agent: Microsoft ADO.NET Data Services
Accept-Charset: UTF-8
DataServiceVersion: 1.0;NetFx
MaxDataServiceVersion: 3.0;NetFx
Accept: application/atom+xml,application/xml
Authorization: WRAP access_token="<token>"
x-ms-version: 1.0
Content-Type: application/xml
Host: integration.zurich.test.dnsdemo1.com:5446
Content-Length: 218
Expect: 100-continue

<uri xmlns="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">https://integration.zurich.test.dnsdemo1.com:5446/test01/$PartnerManagement/X12SchemaReferences(1)</uri>
```

## <a name="BKMK_DeleteSchemaRefLink"></a>Delete Link between X12ProtocolSettings and Other Entities
You can delete a link between an X12ProtocolSettings and other entities using a DELETE HTTP method.

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

