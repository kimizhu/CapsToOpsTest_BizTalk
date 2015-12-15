---
description: na
keywords: na
pagetitle: APPENDIX: Response Codes for X12 Bridges
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75396626-0678-4b6d-b891-0b01e1b290bb
---
# APPENDIX: Response Codes for X12 Bridges
Lists the possible response codes you might encounter when a message is processed using the X12 Receive or X12 Send pipelines in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

|Response Code <br /> <br />|Description <br /> <br />|
|-----------------|---------------|
|200 <br /> <br />|This response code denotes that all the transaction sets in the message/interchange were processed as well as routed successfully. <br /> <br />|
|202 <br /> <br />|This response code denotes that even though all the transaction sets in the messages/interchange were processed successfully, there were errors while routing one or more of them to the success endpoint. However the ones which could be routed to the success endpoint were routed to the suspend endpoint successfully. <br /> <br />|
|206 <br /> <br />|This response code denotes that one or more transaction sets failed processing. The successfully-processed transaction sets are routed to the success endpoint and the others that failed processing are sent to the suspend endpoint. <br /> <br />|
|500 <br /> <br />|This response code denotes all other issues that might be encountered while processing transactions set(s) in a message/interchange. Such a response code is mostly encountered when even the message suspension fails. <br /> <br />|

## See Also
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

