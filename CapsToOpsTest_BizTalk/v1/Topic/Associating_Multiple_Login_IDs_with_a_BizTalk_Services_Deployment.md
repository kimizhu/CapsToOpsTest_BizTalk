---
description: na
keywords: na
pagetitle: Associating Multiple Login IDs with a BizTalk Services Deployment
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce34c646-44a6-48be-a9de-813a39e334d5
---
# Associating Multiple Login IDs with a BizTalk Services Deployment
You can associate multiple accounts with the same [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployment or you can associate multiple [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployments with a single account. This topic provides instructions on how to perform many-to-many association between accounts and [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployments.

> [!IMPORTANT]
> The first time you register, the BizTalk Service deployment is automatically associated with the Microsoft Account (Live.com, Outlook.com, Hotmail.com) or the Work account you are logged in as. Once this association is done, only an account within the same work OR a Microsoft account has access to the BizTalk Services deployment. It cannot be changed.
> 
> **Example**: You registered a BizTalk Service deployment using a Microsoft account (user@live.com). In this scenario, only Microsoft Account users can manage the BizTalk Service using the BizTalk Services portal. A work account cannot be used.
> 
> **Example**: You registered a BizTalk Service deployment using a work account in an Azure Active Directory (user@contoso.com). In this scenario, only Azure Active Directory users within contoso can manage the BizTalk Service using the BizTalk Services portal. A Microsoft account cannot be used.

### To associate multiple accounts with a BizTalk Services deployment

1. If you have not registered the [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployment, refer to [Registering and Updating a BizTalk Service Deployment on the BizTalk Services Portal](/Topic/Registering_and_Updating_a_BizTalk_Service_Deployment_on_the_BizTalk_Services_Portal.md) before continuing.

2. From the Azure classic portal, click **[!INCLUDE[af_integration](/Token/af_integration_md.md)]**, and select the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

3. From the command bar, click **Manage** to launch the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

4. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], click the **Settings** tab, click **Add**, and add the account that you want to associate with the [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployment.

5. To remove an account associated with a [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployment, select the account from the **Settings** tab, and click **Delete**.

### To associate multiple BizTalk Services deployment with a single account

1. From the Azure classic portal, click **[!INCLUDE[af_integration](/Token/af_integration_md.md)]**, and select the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

2. From the command bar, click **Manage** to launch the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

3. Depending on whether the account you logged in with is already associated with any [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscriptions, you will have on of the following two options:

   - If you already have more than one [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription associated with the account you logged in with, you are routed to the **Register Account** page that lists all the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscriptions that are associated with the account you logged in with. From the page, click **Register New Deployment** to register another [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

      - OR -

   - If the account you logged in with is only associated with one [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription, you are directly routed to the **Partners** page in [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. From the top-left corner, click **[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]** logo to open the **Register Account** page. From the page, click **Register New Deployment** to register another [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription with the account you logged in with.

4. In the **Register New Deployment** page, enter the details for the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription that you want to associate with the account.

   |||
   |-|-|
   |**BizTalk Service Name** <br /> <br />|Enter the name for your [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
   |**Issuer name** <br /> <br />|Enter the [!INCLUDE[ac2](/Token/ac2_md.md)] Issuer Name used by your [!INCLUDE[af_integration](/Token/af_integration_md.md)]. The [!INCLUDE[ac2](/Token/ac2_md.md)] Issuer Name is available in the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885) after you sign in. [BizTalk Services: Issuer Name and Issuer Key](http://go.microsoft.com/fwlink/p/?LinkID=303941) lists the steps to retrieve the [!INCLUDE[ac2](/Token/ac2_md.md)] Issuer Name. <br /> <br />The correct Issuer Name must be specified. <br /> <br />|
   |**Issuer secret** <br /> <br />|Enter the [!INCLUDE[ac2](/Token/ac2_md.md)] Issuer Secret (Issuer Key) used by your [!INCLUDE[af_integration](/Token/af_integration_md.md)]. The [!INCLUDE[ac2](/Token/ac2_md.md)] Issuer Secret is available in the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885) after you sign in. [BizTalk Services: Issuer Name and Issuer Key](http://go.microsoft.com/fwlink/p/?LinkID=303941) lists the steps to retrieve the [!INCLUDE[ac2](/Token/ac2_md.md)] Issuer Secret. <br /> <br />|

5. Click **Register**.

6. Once you have registered a single account with multiple [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployments, you can navigate between different deployments. To do so, go to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] registration page by clicking the **[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]** logo and then select the deployment you want to work with.

## See Also
[Using the BizTalk Services Portal](/Topic/Using_the_BizTalk_Services_Portal.md)

