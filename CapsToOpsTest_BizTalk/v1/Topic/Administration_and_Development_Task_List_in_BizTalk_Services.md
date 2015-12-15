---
description: na
keywords: na
pagetitle: Administration and Development Task List in BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-03
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9584b43-20da-4d5e-8fcf-4253941d4c96
---
# Administration and Development Task List in BizTalk Services

## Getting Started
When working with [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], there are several on-premises and cloud-based components to consider. To get started, consider the following process flow:

|Step <br /> <br />|Who’s responsible <br /> <br />|Task <br /> <br />|Related Links <br /> <br />|
|--------|---------------------|--------|-----------------|
|1. <br /> <br />|Administrator <br /> <br />|Create the [!INCLUDE[azure_1](/Token/azure_1_md.md)] Subscription using a Microsoft account or an Organizational account. <br /> <br />|[Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885) <br /> <br />|
|2. <br /> <br />|Administrator <br /> <br />|Create or provision a BizTalk Service. <br /> <br />|[Create a BizTalk Service using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) <br /> <br />|
|3. <br /> <br />|Administrator <br /> <br />|Register you or your company’s [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployment. <br /> <br />|[Registering and Updating a BizTalk Service Deployment on the BizTalk Services Portal](/Topic/Registering_and_Updating_a_BizTalk_Service_Deployment_on_the_BizTalk_Services_Portal.md) <br /> <br />|
|4. Optional <br /> <br />|Administrator <br /> <br />|Applies if the application uses [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] to connect to an on-premises Line-of-Business (LOB) system or uses a Queue or Topic Destination. <br /> <br />Create the [!INCLUDE[azure_2](/Token/azure_2_md.md)][!INCLUDE[sb2](/Token/sb2_md.md)] Namespace. Give this namespace, [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name, and [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Key values to the developer. <br /> <br />|[How to: Create or Modify a Service Bus Service Namespace](http://go.microsoft.com/fwlink/p/?LinkID=248628) <br /> <br />[Get Issuer Name and Issuer Key values](http://go.microsoft.com/fwlink/p/?LinkID=303941) <br /> <br />|
|5. <br /> <br />|Developer <br /> <br />|Install the SDK and create the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)]. <br /> <br />|[Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md) <br /> <br />[Create Rich Messaging Endpoints on Azure](/Topic/Create_Rich_Messaging_Endpoints_on_Azure.md) <br /> <br />|
|6. <br /> <br />|Developer <br /> <br />|Deploy your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] to your BizTalk Service hosted on [!INCLUDE[azure_2](/Token/azure_2_md.md)]. <br /> <br />|[Deploying and Refreshing the BizTalk Services Project](/Topic/Deploying_and_Refreshing_the_BizTalk_Services_Project.md) <br /> <br />|
|7. Optional <br /> <br />|Administrator <br /> <br />|Applies if you are using EDI. <br /> <br />You can add Partners and create Agreements on the [!INCLUDE[tpm_full](/Token/tpm_full_md.md)]. When you create an Agreement, you can add the [!INCLUDE[bridge](/Token/bridge_md.md)] and/or [!INCLUDE[transform](/Token/transform_md.md)]s created by the developer to the Agreement settings. <br /> <br />|[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md) <br /> <br />|
|8. <br /> <br />|Administrator <br /> <br />|Using the [!INCLUDE[azportal](/Token/azportal_md.md)], monitor the health of your BizTalk Service, including performance metrics. <br /> <br />|[BizTalk Services: Dashboard, Monitor and Scale tabs](http://go.microsoft.com/fwlink/p/?LinkID=302281) <br /> <br />|
|9. <br /> <br />|Administrator <br /> <br />|Using the [!INCLUDE[tpm_full](/Token/tpm_full_md.md)], manage the artifacts used by [!INCLUDE[af_integration](/Token/af_integration_md.md)] and track messages as they are processed by the [!INCLUDE[bridge](/Token/bridge_md.md)] files. <br /> <br />|[Using the BizTalk Services Portal](/Topic/Using_the_BizTalk_Services_Portal.md) <br /> <br />|
|10. <br /> <br />|Administrator <br /> <br />|Create a backup plan to back up the BizTalk Service. <br /> <br />|[Business Continuity and Disaster Recovery in BizTalk Services](/Topic/Business_Continuity_and_Disaster_Recovery_in_BizTalk_Services.md) <br /> <br />|

## Next
[Tutorials and Samples](/Topic/Tutorials_and_Samples.md)

[Create the project in Visual Studio](/Topic/Create_the_project_in_Visual_Studio.md)

[Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md)

## See Also
[Create the project in Visual Studio](/Topic/Create_the_project_in_Visual_Studio.md)
[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303664)
[EDI, AS2, and EDIFACT Messaging &#40;Business to Business&#41;](/Topic/EDI,_AS2,_and_EDIFACT_Messaging__Business_to_Business).md)
[Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md)
[Learn and create Message Maps and Transforms](/Topic/Learn_and_create_Message_Maps_and_Transforms.md)
[Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md)

