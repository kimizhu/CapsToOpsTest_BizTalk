---
description: na
keywords: na
pagetitle: EDIFACTProtocolSettings
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0578d0ed-4d75-45ca-8f23-2e88366d21f6
---
# EDIFACTProtocolSettings
An `EDIFACTProtocolSettings` entity inherits the `ProtocolSettings` entity and provides the EDIFACT protocol information.

## EDIFACTProtocolSettings Entity Properties

|Property <br /> <br />|Type <br /> <br />|Description <br /> <br />|
|------------|--------|---------------|
|AcknowledgementControlNumberLowerBound <br /> <br />|Long <br /> <br />|**Required**. Specifies a numeric value for the lower bounds for the acknowledgement control number. The possible values are between 1 and 999999999. <br /> <br />|
|AcknowledgementControlNumberPrefix <br /> <br />|String <br /> <br />|Specifies a prefix for the acknowledgement control number. This value can be alpha-numeric and must not be more than 9 characters. <br /> <br />|
|AcknowledgementControlNumberSuffix <br /> <br />|String <br /> <br />|Specifies a suffix for the acknowledgement control number. This value can be alpha-numeric and must not be more than 9 characters. <br /> <br />|
|AcknowledgementControlNumberUpperBound <br /> <br />|Long <br /> <br />|**Required**. Specifies a numeric value for the upper bounds for the acknowledgement control number. The possible values are between 1 and 999999999. <br /> <br />|
|AcknowledgementControlNumberRollover <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the control number is reset to the lower limit once the maximum value is exceeded. <br /> <br />|
|AllowLeadingAndTrailingSpacesAndZeroes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the EDI interchange fails validation if a data element in the interchange does not conform to its length requirement because of leading (or trailing) zeroes or trailing spaces, but does conform to its length requirement when they are removed. <br /> <br />|
|ApplicationReferenceId <br /> <br />|String <br /> <br />|Specifies the application reference ID. This should not be more than 14 characters. <br /> <br />|
|ApplyDelimiterStringAdvice <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a UNA segment is generated for the interchange. If this is set to true, UNA6 cannot be empty. <br /> <br />|
|BatchFunctionalAck <br /> <br />|Bool <br /> <br />|**Required**. Set this to true to send functional acknowledgements in batches. If set to false, each functional acknowledgement is sent separately. <br /> <br />|
|BatchTechnicalAck <br /> <br />|Bool <br /> <br />|**Required**. Set this to true to send technical acknowledgements in batches. If set to false, each technical acknowledgement is sent separately. <br /> <br />|
|CharacterSet <br /> <br />|Short <br /> <br />|**Required**. Specifies the character set. The valid values are **0** for UNOB, **1** for UNOA, **2** for UNOC, **3** for UNOD, **4** for UNOE, **5** for UNOF, **6** for UNOG, **7** for UNOH,  **8** for UNOI, **9** for  UNOJ, **10** for UNOK,  **11** for UNOX, **12** for UNOY, **13** for KECA. <br /> <br />|
|CheckDuplicateGroupControlNumber <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether interchanges with duplicate group control numbers (UNG5) are processed. <br /> <br />|
|CheckDuplicateInterchangeControlNumber <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether interchanges with duplicate interchange control numbers are processed. This checks the interchange control number for the received interchange with the interchange control number of an earlier message. If a match occurs, the bridge processes the interchange based on the value of this property. <br /> <br />|
|CheckDuplicateTransactionSetControlNumber <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether interchanges with duplicate transaction sets (UNH1) are processed. <br /> <br />|
|CommunicationAgreementId <br /> <br />|String <br /> <br />|Specifies the communication agreement between two partners. <br /> <br />|
|ComponentSeparator <br /> <br />|Int <br /> <br />|**Required**. Specifies the component separator used by the bridge to identify the different components in the message. This value must not be an empty space, an alphabet, or a numeric character. <br /> <br />|
|CreateEmptyXmlTagsForTrailingSeparators <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether empty XML tags are included for trailing separators. <br /> <br />|
|CreateGroupingSegments <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether UNG elements are populated in the message. <br /> <br />|
|DataElementSeparator <br /> <br />|Int <br /> <br />|**Required**. Specifies a single character that the bridge uses to separate composite data elements consisting of two or more simple data elements. <br /> <br />|
|DecimalPointIndicator <br /> <br />|Int <br /> <br />|**Required**. Specifies a single character that is used to denote a decimal point. <br /> <br />|
|DelimiterOverrides <br /> <br />|DataServiceCollection&lt;EDIFACTDelimiterOverride&gt; <br /> <br />|A navigation property that references the delimiter overrides associated with an EDIFACT message. <br /> <br />|
|EnableDefaultGroupHeaders <br /> <br />|Bool <br /> <br />|Specifies whether default group headers are included or not. <br /> <br />|
|EnvelopeOverrides <br /> <br />|DataServiceCollection&lt;EDIFACTEnvelopeOverride&gt; <br /> <br />|A navigation property that references the envelop overrides associated with an EDIFACT message. <br /> <br />|
|FunctionalGroupId <br /> <br />|String <br /> <br />|Specifies the functional group ID. <br /> <br />|
|GenerateLoopForValidMessagesInAck <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the SG1/SG4 loops are generated in the functional CONTRL acknowledgements for accepted transaction sets. <br /> <br />|
|GroupApplicationPassword <br /> <br />|String <br /> <br />|**Required**. Specifies the GroupApplicationPassword property for the EDIFACT message. <br /> <br />|
|GroupApplicationSenderId <br /> <br />|String <br /> <br />|Specifies the GroupApplicationSenderId property for the EDIFACT message. <br /> <br />|
|GroupApplicationSenderQualifier <br /> <br />|String <br /> <br />|Specifies the GroupApplicationSenderQualifier property for the EDIFACT message. <br /> <br />|
|GroupApplicationReceiverQualifier <br /> <br />|String <br /> <br />|Specifies the GroupApplicationReceiverQualifier property for the EDIFACT message. <br /> <br />|
|GroupAssociationAssignedCode <br /> <br />|String <br /> <br />|Specifies the GroupAssociationAssignedCode property for the EDIFACT message. <br /> <br />|
|GroupControllingAgencyCode <br /> <br />|Short <br /> <br />|Specifies the GroupControllingAgencyCode property for the EDIFACT message. <br /> <br />|
|GroupControlNumberLowerBound <br /> <br />|Long <br /> <br />|Specifies a numeric value for the lower bounds for the group control number. The possible values are between 1 and 999999999. <br /> <br />|
|GroupControlNumberPrefix <br /> <br />|String <br /> <br />|Specifies the prefix for the group control number. <br /> <br />|
|GroupControlNumberRollover <br /> <br />|Bool <br /> <br />|Specifies whether the group control number is reset to the lower limit once the maximum value is exceeded. <br /> <br />|
|GroupControlNumberSuffix <br /> <br />|String <br /> <br />|Specifies the suffix for the group control number. <br /> <br />|
|GroupControlNumberUpperBound <br /> <br />|Long <br /> <br />|Specifies a numeric value for the lower bounds for the group control number. The possible values are between 1 and 999999999. This value must be greater than or equal to the value specified for the GroupControlNumberLowerBound. <br /> <br />|
|GroupMessageVersion <br /> <br />|String <br /> <br />|Specifies the message version. <br /> <br />|
|GroupMessageRelease <br /> <br />|String <br /> <br />|Specifies the message release. <br /> <br />|
|InterchangeControlNumberLowerBound <br /> <br />|Long <br /> <br />|**Required**. Specifies a numeric value for the lower bounds for the interchange control number. The possible values are between 1 and 999999999. <br /> <br />|
|InterchangeControlNumberPrefix <br /> <br />|String <br /> <br />|Specifies the prefix for the interchange control number. <br /> <br />|
|InterchangeControlNumberRollover <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the interchange control number is reset to the lower limit once the maximum value is exceeded. <br /> <br />|
|InterchangeControlNumberSuffix <br /> <br />|String <br /> <br />|Specifies the suffix for the interchange control number. <br /> <br />|
|InterchangeControlNumberUpperBound <br /> <br />|Long <br /> <br />|**Required**. Specifies a numeric value for the upper bounds for the interchange control number. The possible values are between 1 and 999999999. This value must be greater than or equal to the value for **InterchangeControlNumberLowerBound**. <br /> <br />|
|InterchangeDuplicatesValidity <br /> <br />|Short <br /> <br />|**Required**. You must set this property if **CheckDuplicateInterchangeControlNumber** property is set to **True**. If set, this property can only take values greater than 0. <br /> <br />|
|IsTestInterchange <br /> <br />|Bool <br /> <br />|**Required**. Set this to true if you want [!INCLUDE[af_integration](/Token/af_integration_md.md)] to indicate that the interchange generated is test data. <br /> <br />|
|MaskSecurityInfo <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the security info is masked. <br /> <br />|
|MessageFilterType <br /> <br />|Short <br /> <br />|Specifies the type of message filter. The valid values are **Include** and **Exclude**. <br /> <br />|
|NeedFunctionalAck <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a functional acknowledgement must be returned to the interchange sender. <br /> <br />|
|NeedTechnicalAck <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a technical acknowledgement must be returned to the interchange sender. <br /> <br />|
|PreserveInterchange <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the bridge preserves an EDI interchange. <br /> <br />|
|ProcessingPriorityCode <br /> <br />|String <br /> <br />|Specifies the code determined by the sender for acknowledgement of the interchange. <br /> <br />|
|ProtocolName <br /> <br />|String <br /> <br />|**Required**. Specifies the protocol name. <br /> <br />|
|ProtocolVersion <br /> <br />|Short <br /> <br />|**Required**. Specifies the EDIFACT protocol version. <br /> <br />|
|ReceiverReverseRoutingAddress <br /> <br />|String <br /> <br />|Specifies the reverse routing address for the receiver. <br /> <br />|
|RecipientReferencePasswordQualifier <br /> <br />|String <br /> <br />|Specifies the password qualifier for the recipient. <br /> <br />|
|RecipientReferencePasswordValue <br /> <br />|String <br /> <br />|Specifies the password value for the recipient password qualifier. <br /> <br />|
|ReleaseIndicator <br /> <br />|Int <br /> <br />|**Required**. This character is used to indicate that the text following contains one of the characters used as a composite, data, or segment separator. Therefore, this character is released from its conventional usage in this instance. <br /> <br />|
|RepetitionSeparator <br /> <br />|Int <br /> <br />|**Required**. This character is used to separate adjacent occurrences of the same repeating data element in a segment. <br /> <br />|
|RouteAckToSendPipeline <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the acknowledgement must be returned by a separate channel. <br /> <br />|
|SchemasReferences <br /> <br />|DataServiceCollection&lt;EDIFACTSchemaReference&gt; <br /> <br />|A navigation property that references the schema used for the EDIFACT protocol settings. <br /> <br />|
|SegmentTerminator <br /> <br />|Int <br /> <br />|**Required**. Specifies a single character that the bridge uses to indicate the end of a segment. This value must not be a space, an alphabet, or a numeric character. <br /> <br />|
|SegmentTerminatorSuffix <br /> <br />|Short <br /> <br />|**Required**. Specifies the character that the bridge uses with the segment terminator. The valid values are: <br /> <br /><ul><li>**00** – for None </li><li>**01** – for CR </li><li>**02** – for LF </li><li>**03** – for CRLF </li> </ul>|
|SenderReverseRoutingAddress <br /> <br />|String <br /> <br />|Specifies the reverse routing address of the sender. <br /> <br />|
|SuspendInterchangeOnError <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the entire message is suspended if one or more transaction sets in the interchange fail validation. <br /> <br />|
|TrailingSeparatorPolicy <br /> <br />|Short <br /> <br />|**Required**. Specifies how to process trailing separators. <br /> <br /><ul><li>Set this to **0** (for Not Allowed). If set to 0, trailing delimiters and separators are not allowed in an interchange received from the interchange sender. If the interchange contains trailing delimiters and separators, it will be declared invalid. </li><li>Set this to **1** (for Optional). If set to 1, the bridge accepts interchanges with or without trailing delimiters and separators. </li><li>Set this to **2** (for Mandatory). If set to 2, the received interchange must contain trailing delimiters and separators. </li> </ul>|
|TSApplyNewId <br /> <br />|Bool <br /> <br />|**Required**. <br /> <br />|
|TSControlNumberLowerBound <br /> <br />|Int <br /> <br />|**Required**. Specifies a numeric value for the lower bounds for the transaction set control number. The possible values are between 1 and 999999999. <br /> <br />|
|TSControlNumberPrefix <br /> <br />|String <br /> <br />|Specifies a prefix for the transaction set control number. This value can be alpha-numeric. <br /> <br />|
|TSControlNumberRollover <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the control number is reset to the lower limit once the maximum value is exceeded. <br /> <br />|
|TSControlNumberSuffix <br /> <br />|String <br /> <br />|Specifies a suffix for the transaction set control number. This value can be alpha-numeric. <br /> <br />|
|TSControlNumberUpperBound <br /> <br />|Int <br /> <br />|**Required**. Specifies a numeric value for the upper bounds for the transaction set control number. The possible values are between 1 and 999999999. <br /> <br />|
|UseDotAsDecimalIndicator <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether a dot (.) is used as a decimal separator. <br /> <br />|
|ValidateCharacterSet <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether the character set must be validated. <br /> <br />|
|ValidateEdiTypes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether EDI (data element) validation is enabled on the interchange receiver. <br /> <br />|
|ValidateXSDTypes <br /> <br />|Bool <br /> <br />|**Required**. Specifies whether extended validation (XSD) is enabled on the interchange receiver. <br /> <br />|
|ValidationOverrides <br /> <br />|DataServiceCollection&lt;EDIFACTValidationOverride&gt; <br /> <br />|A navigation property that references EDIFACT validation overrides associated with the instance of EDIFACT protocol settings. <br /> <br />|
|Version <br /> <br />|Byte[] <br /> <br />|This value is auto-generated and is for internal use only. <br /> <br />|

## See Also
[TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md)

