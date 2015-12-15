---
description: na
keywords: na
pagetitle: BizTalk Services tasks in Azure Classic Portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-03
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0399b6b1-86c6-47bf-8793-994010915a92
---
# BizTalk Services tasks in Azure Classic Portal
This topic explains the [!INCLUDE[af_integration](/Token/af_integration_md.md)] tasks in the [!INCLUDE[azportal](/Token/azportal_md.md)].

There are two portals: [!INCLUDE[azportal](/Token/azportal_md.md)] and the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal. This topic focuses on the [!INCLUDE[azportal](/Token/azportal_md.md)] tasks specific to [!INCLUDE[af_integration](/Token/af_integration_md.md)].

One of the first steps in using [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] is to **determine your application needs**. For example:

- Will your business transactions grow over time?

- Are there peak times when your business needs more processing resources? Are there times when your business needs less processing resources?

- Do you have multiple EDI partners and require multiple agreements with these partners?

- Does your application get or put data in an on-premises system, like SQL Server or Oracle?

The answers to these questions and more determine which [!INCLUDE[af_integration](/Token/af_integration_md.md)] edition is right for you. Relevant link:

[BizTalk Services: Editions Chart](http://azure.microsoft.com/documentation/articles/biztalk-editions-feature-chart/)

After you determine your application needs, you **create the BizTalk Service** in the [!INCLUDE[azportal](/Token/azportal_md.md)]. This BizTalk Service hosts and runs your deployed applications (created in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)]). You can have one BizTalk Service or many BizTalk Services; the choice depends on your design needs and wants. Many users have multiple BizTalk Services. Relevant link:

[Create a BizTalk Service using Azure classic portal](http://azure.microsoft.com/documentation/articles/biztalk-provision-services/)

When the BizTalk Service is created, **a deployment URL and security-related user/key pairs are created**. This deployment URL is your online link to your BizTalk Service on [!INCLUDE[azure_1](/Token/azure_1_md.md)]. There are two sets of User/Key pairs:

- [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name and issuer key

- [!INCLUDE[sb2](/Token/sb2_md.md)] issuer name and issuer key

You share the deployment URL and these user/key pairs with your developer to deploy the [!INCLUDE[af_integration](/Token/af_integration_md.md)] project. Relevant link:

[BizTalk Services: Issuer Name and Issuer Key](http://azure.microsoft.com/documentation/articles/biztalk-issuer-name-issuer-key/)

After the project is deployed and running on [!INCLUDE[azure_1](/Token/azure_1_md.md)], you can **monitor the status and performance** of the BizTalk Service. For example, you can:

- Determine if the BizTalk Service is started or stopped.

- See how many messages are sent or received.

- Create a backup of the BizTalk Service.

- View the properties of your BizTalk Service, including the deployment URL and the user/key pairs.

Relevant link:

[BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs](http://azure.microsoft.com/documentation/articles/biztalk-dashboard-monitor-scale-tabs/)

## See Also
[Microsoft Azure BizTalk Services home page](http://azure.microsoft.com/documentation/services/biztalk-services/)

