---
description: na
keywords: na
pagetitle: Registering and Updating a BizTalk Service Deployment on the BizTalk Services Portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-03
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c9bae82-8d07-45df-bf51-b0b31417a9d4
---
# Registering and Updating a BizTalk Service Deployment on the BizTalk Services Portal
When you ‘register’ a BizTalk Service, you are associating your BizTalk Service (and its Issuer Name and Issuer Key) with your project deployments in the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal.

This topic lists your registration options and the steps to register your BizTalk Service in the [!INCLUDE[af_integration](/Token/af_integration_md.md)].

## Before you Begin

- When registration occurs, the BizTalk Service deployment is automatically associated with the Organization account or Microsoft Account you are logged in as. When this association is done, only an organization account or Microsoft account has access to the BizTalk Services deployment. It cannot be changed.

   **Example**: You are logged in as user@contoso.com (an organizational account) when the BizTalk Services deployment is registered. If user@live.com logs in, this user **cannot** access the BizTalk Services deployment. Only users within the same organization (@contoso.com) can view and manage the BizTalk Services deployment.

   **Example**: The same for Microsoft accounts (@live.com, @hotmail.com, and @outlook.com). For example, you are logged in as user@live.com (a Microsoft account) when the BizTalk Services deployment is registered. If user@outlook.com (a Microsoft account) logs in, this user **can** access and manage the BizTalk Services deployment. If user@contoso.com (an organizational account) logs in, this user **cannot** access the BizTalk Services deployment. Only users with a Microsoft account can view and manage the BizTalk Services deployment.

   > [!IMPORTANT]
   > Users (user@live.com or user@contoso.com) can be added as guests in an Azure Active Directory (user@fabrikam.com). These Guests cannot access the BizTalk Services deployment.

- The schemas that conform to the X12 4010 and 5010 standards are available at [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057).

- If messages will be signed and encrypted, a private certificate (.pfx) and a public certificate (.cer) are needed. For information on importing certificates, see [APPENDIX: BizTalk Services Certificates Overview](/Topic/APPENDIX__BizTalk_Services_Certificates_Overview.md).

- If you are using bridges and transforms as part of your solution, you must also install the [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK. You can use the SDK to create these artifacts that might be required while configuring agreements. For more information, see [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md).

## Register with the Portal
> [!IMPORTANT]
> If you registered a [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription with the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] for the Preview release of [!INCLUDE[af_integration](/Token/af_integration_md.md)], you must re-register the subscription for the current release. Note that the artifacts, partners, agreements, etc. that you created or deployed in the Preview registration will be preserved in the new registration as well.

When the BizTalk Service is ‘registered’, you are proving ownership to the BizTalk Service by providing the [!INCLUDE[ac2](/Token/ac2_md.md)] Issuer Name and Issuer Key.

There are two options to register your BizTalk Service:

**OPTION 1: Automatically register by clicking “Manage”**

When you create a BizTalk Service in the [!INCLUDE[azportal](/Token/azportal_md.md)] and you then select **Manage** for the first time, your BizTalk Service (and its Issuer Name and Issuer Key) is automatically registered in the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal.

If access to your deployments uses Organizational accounts, then log into the [!INCLUDE[azportal](/Token/azportal_md.md)] as your organizational account, create the BizTalk Service, and then click **Manage** to automatically register. If access to your deployments uses Microsoft accounts, then log into the [!INCLUDE[azportal](/Token/azportal_md.md)] as your Microsoft account, create the BizTalk Service, and then click **Manage** to automatically register.

**OPTION 2: Automatically register using the BizTalk Service portal**

You create a BizTalk Service in the [!INCLUDE[azportal](/Token/azportal_md.md)] and you do **not** select **Manage**. To automatically register the BizTalk Service, log in to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal ( HYPERLINK "https://YourBizTalkServiceName.portal.biztalk.windows.net/" https://YourBizTalkServiceName.portal.biztalk.windows.net/) using the same account (Microsoft or Organizational) that created the BizTalk Service. Logging in with this same account automatically registers the BizTalk Service.

If access to your deployments uses Organizational accounts, then log into the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal as the organizational account to automatically register. If access to your deployments uses Microsoft accounts, then log into the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal as the Microsoft account to automatically register.

**Additional**

When you log into the [!INCLUDE[azportal](/Token/azportal_md.md)] to provision a [!INCLUDE[af_integration](/Token/af_integration_md.md)], you are logged in with a specific Microsoft or Organizational account. You can add additional accounts to manage the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. You can also associate a single Microsoft or Organizational account with multiple [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscriptions. To achieve this many-to-many association, see [Associating Multiple Login IDs with a BizTalk Services Deployment](/Topic/Associating_Multiple_Login_IDs_with_a_BizTalk_Services_Deployment.md).

[Create a BizTalk Service using Azure classic portal](http://azure.microsoft.com/documentation/articles/biztalk-provision-services/)

## Next
[Associating Multiple Login IDs with a BizTalk Services Deployment](/Topic/Associating_Multiple_Login_IDs_with_a_BizTalk_Services_Deployment.md)

[Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md)

[Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md)

## See Also
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

