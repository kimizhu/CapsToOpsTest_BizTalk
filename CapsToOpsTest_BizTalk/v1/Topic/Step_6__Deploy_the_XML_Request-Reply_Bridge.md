---
description: na
keywords: na
pagetitle: Step 6: Deploy the XML Request-Reply Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f764375-6615-4a14-8904-a2ced90c6a9c
---
# Step 6: Deploy the XML Request-Reply Bridge
This topic in the tutorial provides instructions on how to deploy the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. We have already deployed the two relay services to the [!INCLUDE[sb2](/Token/sb2_md.md)].

### To deploy the XML Request-Reply bridge

1. In [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)], right-click the BizTalk Service solution, and select **Build**.

2. After a successful build, right-click the solution name again, and then select **Deploy** to open the deployment dialog box. Enter the following properties:

   |Property Name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |**Deployment Endpoint** <br /> <br />|A read-only field that displays the BizTalk Service URL and the default namespace specified in [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. <br /> <br />|
   |**Acs Namespace** <br /> <br />|Enter the Access Control namespace for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
   |**Issuer Name** <br /> <br />|Enter the username who is the owner of the service namespace you specified, or has manage claims to the namespace. This property is required to authenticate the identity of the user to the [!INCLUDE[sb2](/Token/sb2_md.md)]. <br /> <br />|
   |**Shared Secret** <br /> <br />|Enter the secret key for authentication of the service namespace owner. <br /> <br />|

3. Select **Deploy**. The [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] Output pane displays the deployment progress and result. The URL where the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] is deployed is also displayed in the Output pane.

## See Also
[Tutorial: Using BizTalk Service Bridges to Send and Receive Messages from Service Bus Relay Service](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md)

