---
description: na
keywords: na
pagetitle: Manage your Resources in BizTalk Services portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69a4f82d-c339-4780-8761-29f2dd37cd10
---
# Manage your Resources in BizTalk Services portal
View the [!INCLUDE[bridge](/Token/bridge_md.md)]s, schemas, Transforms, Certificates, and Assemblies used by your application.

Once you have deployed your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], you can view these items and resources in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. The X12 and AS2 bridges deployed as part of the agreements are also listed here.

You can use the **Resources** tab on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page to do the following:

- [Schemas](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md#BKMK_Schemas): Add EDI schemas (.xsd) to be used by the different message types, like 850-Purchase Order.

- [Transforms](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md#BKMK_Trfm): Add [!INCLUDE[transform](/Token/transform_md.md)]s (.trfm) created by the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] developer to manipulate customer data.

- [Certificates](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md#BKMK_Certs): Upload and store SSL certificates added when configuring a partner, partner profile, and AS2.

- [Assemblies](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md#BKMK_Assembly): Add user assemblies that are used within transforms.

## Bridges
From the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], select the **Bridges** tab. You can:

- **Search for a [!INCLUDE[bridge](/Token/bridge_md.md)]** – If you have a lot of [!INCLUDE[bridge](/Token/bridge_md.md)]s deployed, the list can run into pages. You can search for a [!INCLUDE[bridge](/Token/bridge_md.md)] by typing the name of the [!INCLUDE[bridge](/Token/bridge_md.md)] in the **Search** text box. The search results are instantaneous and display the names that match the search string you enter.

- **Delete a [!INCLUDE[bridge](/Token/bridge_md.md)]** – To delete a [!INCLUDE[bridge](/Token/bridge_md.md)], select the [!INCLUDE[bridge](/Token/bridge_md.md)], and then select **Delete**.

   > [!NOTE]
   > Deleting the bridge does not delete the artifacts associated with the bridge, or other bridges that this bridge is associated to.

## <a name="BKMK_Schemas"></a>Schemas
To add a schema, go to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page and select **Resources**. In the **Schemas** tab, select **Upload** to browse to the schema (.xsd). If another schema with the same file name is uploaded at the same location, you get a warning message and depending on the option you chose, the second schema overwrites the first schema.

When the schemas are added, the schema can be specified as the **Message Type** in the X12 General Settings ([Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md)) and the AS2 General Settings ([Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md)).

Schemas can be customized in the Schema Editor. To use the Schema Editor:

1. Open a [!INCLUDE[af_integration](/Token/af_integration_md.md)] project in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)].

2. Add an existing schema (.xsd) or add a new schema (.xsd) to the project. Right-click the project and select **Add**. Select **Existing Item** to add a schema that is already created. To create a new schema, select **New Item** and then select **Schema**.

3. Select **Add**.

4. Double-click the schema (.xsd) to open the Schema Editor.

At this point, records, attributes, elements and groups can be added. [Developing EDI Schemas](http://go.microsoft.com/fwlink/p/?LinkId=248181) provides information on creating and modifying existing schemas.

## <a name="BKMK_Trfm"></a>Transforms
To add a [!INCLUDE[transform](/Token/transform_md.md)] (.trfm), go to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page and select **Resources**. In the [!INCLUDE[transform](/Token/transform_md.md)]s tab, select **Upload** and select your [!INCLUDE[transform](/Token/transform_md.md)] file (.trfm). If another transform with the same file name is uploaded at the same location, you get a warning message and depending on the option you chose, the second transform overwrites the first transform.

[!INCLUDE[transform](/Token/transform_md.md)]s can also be added when configuring an agreement.

## <a name="BKMK_Certs"></a>Certificates
The Certificates tab enables you to view as well as upload certificates. To see the added certificates, go to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page and select **Resources**. Select the **Certificates** tab to see the certificates that have been added. If the certificate with the same thumbprint is uploaded again, you get a warning message and depending on the option you chose, the second certificate overwrites the first certificate.

To add a certificate, from the **Certificates** tab, select **Upload** and browse to the certificate to be uploaded. A trading partner’s public certificate (CertificateName.cer) or your own private certificate (CertificateName.pfx) with the password can be used.

## <a name="BKMK_Assembly"></a>Assemblies
To add custom user assemblies (.dll) that might be referenced within transforms, go to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page and select **Resources**. In the  **Assemblies** tab, select **Upload** and select the user assemblies to be uploaded.

## Known Issue
When adding **Resources**, the dialog window may not remember the path previously used to add a resource. To remember the previously-used path, try adding the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] web site to **Trusted Sites** in Internet Explorer.

## See Also
[Tracking Messages in BizTalk Services portal](/Topic/Tracking_Messages_in_BizTalk_Services_portal.md)
[Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md)
[Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md)
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

