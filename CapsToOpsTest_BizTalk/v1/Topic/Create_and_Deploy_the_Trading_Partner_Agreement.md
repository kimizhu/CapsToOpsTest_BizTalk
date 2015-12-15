---
description: na
keywords: na
pagetitle: Create and Deploy the Trading Partner Agreement
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5639fe04-a9a1-40ce-8f98-132b5d4775a0
---
# Create and Deploy the Trading Partner Agreement
This part of the tutorial builds the EDI scenario. To build the EDI scenario, Northwind uses the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to create trading partners and agreements. Contoso sends the sales order as an X12 message to the deployed agreement. After receiving the X12 sales order, the deployed agreement processes the message, transforms it to the **SalesOrder** format expected by the EAI [!INCLUDE[bridge](/Token/bridge_md.md)], and routes it to the EAI [!INCLUDE[bridge](/Token/bridge_md.md)] that you already deployed earlier. The [!INCLUDE[bridge](/Token/bridge_md.md)] then inserts the message into the **SalesOrder** table using the SQL [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. The topics in this section lists the steps to build and test the EDI scenario for the tutorial.

## In This Section

- [Step 1: Add the X12 SalesOrder &#40;840&#41; Schema and Transform to the Visual Studio Project](/Topic/Step_1__Add_the_X12_SalesOrder__840)%20Schema%20and%20Transform%20to%20the%20Visual%20Studio%20Project.md)

- [Step 2: Create Partners in the Azure BizTalk Portal](/Topic/Step_2__Create_Partners_in_the_Azure_BizTalk_Portal.md)

- [Step 3: Create Agreements Between Partner Profiles](/Topic/Step_3__Create_Agreements_Between_Partner_Profiles.md)

- [Step 4: Test the EDI Solution](/Topic/Step_4__Test_the_EDI_Solution.md)

## See Also
[Tutorials and Samples](/Topic/Tutorials_and_Samples.md)

