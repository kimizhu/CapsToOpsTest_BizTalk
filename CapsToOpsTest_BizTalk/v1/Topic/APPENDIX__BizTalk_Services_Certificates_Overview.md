---
description: na
keywords: na
pagetitle: APPENDIX: BizTalk Services Certificates Overview
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-03
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3b8d534-fc79-4203-8f09-cd3ac3510675
---
# APPENDIX: BizTalk Services Certificates Overview
In [!INCLUDE[af_integration](/Token/af_integration_md.md)], certificates are used in several areas:

- [Create a BizTalk Service using Azure classic portal](http://azure.microsoft.com/documentation/articles/biztalk-provision-services/): A public certificate (.cer) is automatically created. You can download the certificate and install it on your test/development environment. In production, use a signed certificate; which can be uploaded it to your BizTalk Service in the [!INCLUDE[azportal](/Token/azportal_md.md)].

- [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md): Can be a private certificate (.pfx) or a public certificate (.cer).

- [Certificates](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md#BKMK_Certs): Lists all the private (.pfx) and public (.cer) certificates added for agreements between partners.

- AS2 Receive Settings ([Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md)): A certificate is used for message signing and encryption. If the message is signed, a public certificate (.cer) is needed. If the message is encrypted, a private certificate (.pfx) and its password are needed.

- AS2 Send Settings ([Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md)): A certificate is used for message signing and encryption. If the message is signed, a private certificate (.pfx) and its password are needed. If the message is encrypted, a public certificate (.cer) is needed.

## Install the test certificate
When you create a BizTalk Service in the [!INCLUDE[azportal](/Token/azportal_md.md)], a public certificate is automatically created that is self-signed and should only be used in test/development environments. You can use this certificate to secure the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] (BAS) runtime website. See [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) for details on the website.

This section lists the steps to install the certificate into the **Trusted Root Certification Authorities** store on your computer:

1. In the [!INCLUDE[azportal](/Token/azportal_md.md)], select your BizTalk Service, and select the **Dashboard** tab. In **quick glance**, download the SSL certificate.

2. Copy the certificate to your test/development machine with the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK installed. This is a public certificate (.cer).

3. On your test/development machine, double-click the .cer file. Select **Install Certificate**.

4. Select **Place all certificates in the following store**, select **Browse**, and select **Trusted Root Certification Authorities**.

5. Complete the installation. You’ll get a Security Warning; which is normal. Select **Yes**.

## .p7b certificates
A certificate may also have a .p7b extension. In this scenario, import the .p7b certificate, and then export it to a .pfx or .cer format using the following steps.

#### To import a .p7b certificate

1. Open the Microsoft Management Console (MMC.exe): In the **Run** window, type **mmc.exe**.

2. In the MMC, go to the **File** menu, and select **Add/Remove Snap-in**.

3. In **Available snap-ins**, select **Certificates**, and select **Add**. Select **My user account**, **Service account** or **Computer account**. Choose any option. We are importing the .p7b certificate *only* so we can export it.

   Select **OK**.

4. Expand **Certificates** and choose any folder. For example, select **Personal**. We are importing the .p7b certificate *only* so we can export it in a .cer or .pfx format.

5. Right-click the folder, select **All Tasks**, and select **Import**. The Certificate Import Wizard opens:

   - Select Next.

   - Browse to the .p7b certificate file. In the Open window, select **All Files** from the filter drop-down, and then select the .p7b certificate.

      Select **Next**.

   - Select the **Certificate store** to put the .p7b certificate. For example, select **Personal**.

   - Select **Finish**.

   Expand the Certificate store folder. The imported .p7b certificate is now displayed in the Certificates folder.

Once imported, the .p7b certificate can now be exported to a .cer or .pfx format.

#### To export a .p7b certificate as .cer or .pfx

1. Right-click the imported .p7b certificate, select **All Tasks**, and select **Export**. The Certificate Import Wizard opens:

   - Select Next.

   - Select the .CER or .PFX option. To determine which option to choose, see [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md) or [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md).

      Select **Next**.

   - **Browse** to the path to store the exported certificate and enter a **File name**. select **Save**.

   - Select **Next** and then select **Finish** to close wizard.

2. The exported certificate resides in the folder you entered.

When a certificate is exported in the MMC, the original certificate remains in the certificate store.

## See Also
[Registering and Updating a BizTalk Service Deployment on the BizTalk Services Portal](/Topic/Registering_and_Updating_a_BizTalk_Service_Deployment_on_the_BizTalk_Services_Portal.md)
[Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md)
[Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md)
[Manage your Resources in BizTalk Services portal](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md)
[Tracking Messages in BizTalk Services portal](/Topic/Tracking_Messages_in_BizTalk_Services_portal.md)
[Configuring Agreements from a BizTalk perspective](/Topic/Configuring_Agreements_from_a_BizTalk_perspective.md)
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

