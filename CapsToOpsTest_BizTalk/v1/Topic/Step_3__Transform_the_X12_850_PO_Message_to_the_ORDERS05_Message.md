---
description: na
keywords: na
pagetitle: Step 3: Transform the X12 850 PO Message to the ORDERS05 Message
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.service: multiple
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4478d0f1-5fff-4ffe-a5ef-92ef7e451299
---
# Step 3: Transform the X12 850 PO Message to the ORDERS05 Message
Both the X12 850 schemas and ORDERS05 schemas are pretty complex and require functional expertise in the respective domains to understand and create maps between the two schemas. While you already generated the schema for ORDERS05 IDOC, you can get the schema for X12 PO message (X12_00401_850.xsd) from the **MicrosoftEdiXSDTemplates.zip** that you previously downloaded and extracted. You must add the **X12_00401_850.xsd** schema to the **SAPIntegration** project.

Creating a [!INCLUDE[transform](/Token/transform_md.md)] between the X12 850 PO and ORDERS05 PO requires functional domain knowledge of both the X12 schema and the ORDERS05 schema. Only then one can identify which field in the X12 schema maps to which field in the ORDERS05 schema. In this tutorial, we do not get into such details and instead use an existing [!INCLUDE[transform](/Token/transform_md.md)] (**AzureTransformations.trfm**) between these two schemas. This [!INCLUDE[transform](/Token/transform_md.md)] is available in the **SAPIntegration** project that you can download from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=241990).

To include the transform in the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], right-click the project name, select **Add**, select **Existing Items**, and then navigate to the location where you downloaded the **SAPIntegration** sample from the MSDN Code Gallery. Select the **AzureTransformations.trfm** and then select **Add**.

## See Also
[Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server](/Topic/Tutorial__Using_Azure_BizTalk_Services_to_Integrate_with_an_On-Premises_SAP_Server.md)

