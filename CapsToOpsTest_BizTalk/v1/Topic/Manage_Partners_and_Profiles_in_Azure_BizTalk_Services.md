---
description: na
keywords: na
pagetitle: Manage Partners and Profiles in Azure BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b993139-3261-49b2-a778-f46aee74365b
---
# Manage Partners and Profiles in Azure BizTalk Services
The Partners page displays the list of partners with their name, email, phone, and description. Using this page, you can add or delete partners and their profiles.

It is important to understand the concept of a **Service Provider** and a **Partner**. The **Service Provider**  is you or your company. A **Partner** is whomever you receive or send EDI files, which can include another company, another department within your company, and so on. Pipelines are deployed for the **Hosted Partner** when the agreement is deployed. Receive and Send settings are oriented to the context of the **Hosted Partner**. For example, the receive settings in an agreement determine how the **Hosted Partner** receives messages sent from a **Guest Partner**. Likewise, the send settings on the agreement indicate how the **Hosted Partner** sends messages to the **Guest Partner**.

In this topic:

[Add a new partner](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md#BKMK_AddPartner)

[Add or Edit a profile for a partner](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md#BKMK_AddProfile)

[Add a certificate](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md#BKMK_AddCertificate)

## <a name="BKMK_AddPartner"></a>Add a new partner
After you register yourself as the service provider, you can add or delete trading partners in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Partners**.

2. In Partners, click **Add**.

3. In **New Partner**, enter the following:

   |||
   |-|-|
   |Partner name <br /> <br />|**Required**. Enter the name of the partner. The name must be unique. <br /> <br />|
   |Description <br /> <br />|Enter a note or description for the partner. <br /> <br />|
   |First name <br /> <br />|Enter the first name of the primary contact in the partner organization. <br /> <br />|
   |Last name <br /> <br />|Enter the last name of the primary contact in the partner organization. <br /> <br />|
   |Email ID <br /> <br />|Enter the email ID of the primary contact in the partner organization. <br /> <br />|
   |Phone <br /> <br />|Enter the phone number of the primary contact in the partner organization. <br /> <br />|
   |Website URL <br /> <br />|Enter the website of the partner organization. <br /> <br />|
   |Country <br /> <br />|Enter the country/region of the partner organization. <br /> <br />|
   |Address (Line1) <br /> <br />|Enter the address of the partner organization. <br /> <br />|
   |Address (Line2) <br /> <br />|Enter any additional address information of the partner organization. <br /> <br />|
   |City <br /> <br />|Enter the city of the partner organization. <br /> <br />|
   |State <br /> <br />|Enter the state of the partner organization. <br /> <br />|
   |Postal Code <br /> <br />|Enter the postal zip code of the partner organization. <br /> <br />|

4. Click **Save** to add the partner.

When the partners are added, profiles are created automatically.

> [!IMPORTANT]
> When you add you or your company as a Service Provider, you are not automatically added as a Partner. This feature allows you to add multiple partners as the Hosted Partner or Guest Partner, including creating agreements between multiple partners.

**To Delete a Partner**:

Select the row listing the partner that you want to delete and then select **Delete**.

> [!IMPORTANT]
> You cannot delete a partner unless all the profiles and all the agreements for that partner are deleted.

## <a name="BKMK_AddProfile"></a>Add or Edit a profile for a partner
Profiles are organization-specific settings that can correspond to organizational divisions. For example, a partner retail organization named Contoso has an “Electronics” division that accepts orders for electronics inventory. This Electronics division submits requests for electronics supplies to a partner. Contoso also has an “Apparel” division that accepts orders for clothing and then submits requests for clothing supplies to a partner. In this scenario, two profiles for the Contoso partner organization are created: “Contoso Electronics” and “Contoso Apparel”.

A default profile is always created when a partner is added. Profiles can be changed.

1. On the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Partners**.

2. Click on the partner name to open the **Profiles** page for the partner.

   > [!NOTE]
   > To return to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click the back button in the upper left corner.

3. Click **Add** to create a new profile, or click the existing profile.

4. In the **new profile** page, enter the follow information:

   |||
   |-|-|
   |Profile Name <br /> <br />|**Required**. Enter a unique name for the profile. <br /> <br />|
   |Description <br /> <br />|**Optional**. Enter information that describes this particular profile, like “Contoso Electronics”. <br /> <br />|
   |Identities <br /> <br />|Add any identity qualifier values to be used with this profile by clicking **+**. Choose a qualifier code from the drop down list and enter the value. <br /> <br />|
   |Certificates <br /> <br />|A certificate can be added *after* a profile is created and saved. Certificates in the profile can be used for digital signatures with AS2. <br /> <br />|

5. Click **Save**.

When the Partner and Profile are complete, an Agreement can be created. See [Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md).

**To Delete a Profile**:

Select the partner that has the profile you want to delete. Then select the row listing the profile, and then select **Delete**.

## <a name="BKMK_AddCertificate"></a>Add a certificate
Once a profile is saved, you can add a certificate to that profile. Certificates in a partner’s profile are used for message signing and encryption/decryption.

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Partners**, click the Partner name, and then click the profile.

2. In the Certificates section, click **Add**.

3. **Browse** to the location of the certificate file. A trading partner’s public certificate (*CertificateName*.cer) or your own private certificate (*CertificateName*.pfx) can be used.

   Private certificates (.pfx) are password protected. If you are adding a private certificate (.pfx), enter the **Password**.

4. Click **Save**.

> [!TIP]
> To see the added certificates, select **Resources** on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, and then select **Certificates**. The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] also provides notifications for expired certificates.

For information on importing certificates on the computer, see [APPENDIX: BizTalk Services Certificates Overview](/Topic/APPENDIX__BizTalk_Services_Certificates_Overview.md).

## Next
[Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md)

## See Also
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

