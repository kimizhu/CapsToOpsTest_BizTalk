---
description: na
keywords: na
pagetitle: APPENDIX: Promoting Message Properties
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e377692-bad3-4781-98f0-64d81e6316d4
---
# APPENDIX: Promoting Message Properties
Use [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to promote message properties. These properties are used by the agreement for processing such as message routing and batch configuration. There are two types of promoted properties – user-promoted properties and system-promoted properties. User-promoted properties are the properties that the users promote. These properties are defined as part of the agreement, both for the send and receive side. For information, see [Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md).

System-promoted properties are the properties that are promoted by X12/AS2 bridges and are available to users. The following table lists the system-promoted X12 and AS2 properties. Just like the user-defined properties, you can use these properties as well for message routing and batch configuration.

|X12 Send <br /> <br />|
|------------|
|InterchangeDate <br /> <br />|
|InterchangeTime <br /> <br />|
|ReceiverID <br /> <br />|
|ReceiverQualifier <br /> <br />|
|SenderID <br /> <br />|
|SenderQualifier <br /> <br />|
|AgreementID <br /> <br />|
|SystemRequestID <br /> <br />|
|MessageReceivedTime <br /> <br />|
|SourceType <br /> <br />|
|ErrorDescription <br /> <br />|
|EDI.GE01 <br /> <br />|
|EDI.IEA01 <br /> <br />|

|X12 Receive <br /> <br />|
|---------------|
|ISA05 <br /> <br />|
|ISA06 <br /> <br />|
|ISA07 <br /> <br />|
|ISA08 <br /> <br />|
|ISA09 <br /> <br />|
|ISA10 <br /> <br />|
|ISA12 <br /> <br />|
|ISA13 <br /> <br />|
|ISA14 <br /> <br />|
|ISA15 <br /> <br />|
|ISA_Segment <br /> <br />|
|GS01 <br /> <br />|
|GS02 <br /> <br />|
|GS03 <br /> <br />|
|GS04 <br /> <br />|
|GS05 <br /> <br />|
|GS06 <br /> <br />|
|GS07 <br /> <br />|
|GS08 <br /> <br />|
|GE01 <br /> <br />|
|GS_Segment <br /> <br />|
|ST01 <br /> <br />|
|ST02 <br /> <br />|
|ST03 <br /> <br />|
|MessageType <br /> <br />|
|TA1_TA104 <br /> <br />|
|ReuseEnvelope <br /> <br />|
|IsSystemGeneratedAck <br /> <br />|
|AK901 <br /> <br />|
|Exception <br /> <br />|
|InterchangeControlNo <br /> <br />|
|InterchangeDate <br /> <br />|
|InterchangeTime <br /> <br />|
|ReceiverID <br /> <br />|
|ReceiverQualifier <br /> <br />|
|SenderID <br /> <br />|
|SenderQualifier <br /> <br />|
|TsSequenceNumberInGroup <br /> <br />|
|AgreementID <br /> <br />|
|IsInterchange <br /> <br />|
|IsTransactionSet <br /> <br />|
|IsInterchangeAck <br /> <br />|
|IsFunctionalAck <br /> <br />|
|SystemTrackingID <br /> <br />|
|SystemRequestID <br /> <br />|
|MessageReceivedTime <br /> <br />|
|SourceType <br /> <br />|
|SourceName <br /> <br />|

|AS2 Receive <br /> <br />|
|---------------|
|ISA5 <br /> <br />|
|ISA6 <br /> <br />|
|ISA7 <br /> <br />|
|ISA8 <br /> <br />|
|AS2From **Note:** If the AS2 Receive bridge routes messages to an HTTP destination, this property shows up as AS2-From in the HTTP headers. <br />|
|AS2To **Note:** If the AS2 Receive bridge routes messages to an HTTP destination, this property shows up as AS2-To in the HTTP headers. <br />|
|FileName <br /> <br />|
|MessageReceivedTime <br /> <br />|
|SourceType <br /> <br />|
|SourceName <br /> <br />|
|SystemRequestID <br /> <br />|
|AgreementID <br /> <br />|

|EDIFACT <br /> <br />|
|-----------|
|UNA_Segment <br /> <br />|
|UNB_Segment <br /> <br />|
|UNB2_1 <br /> <br />|
|UNB2_2 <br /> <br />|
|UNB2_3 <br /> <br />|
|UNB2_4 <br /> <br />|
|UNB3_1 <br /> <br />|
|UNB3_2 <br /> <br />|
|UNB3_3 <br /> <br />|
|UNB3_4 <br /> <br />|
|UNB11 <br /> <br />|

## See Also
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

