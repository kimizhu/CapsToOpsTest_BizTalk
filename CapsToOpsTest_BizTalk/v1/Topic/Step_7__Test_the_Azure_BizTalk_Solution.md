---
description: na
keywords: na
pagetitle: Step 7: Test the Azure BizTalk Solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 804816a7-f1f9-4afa-bd0c-ee75cedaba06
---
# Step 7: Test the Azure BizTalk Solution
Test the [!INCLUDE[af_integration](/Token/af_integration_md.md)] EAI scenario by sending a XML sales order message to the endpoint where the [!INCLUDE[request_response](/Token/request_response_md.md)] is deployed.

### To send a message to the bridge

1. Download the **MessageSender** tool from [Azure BizTalk Services Samples](http://go.microsoft.com/fwlink/p/?LinkId=303933).

2. Build the project and use the resulting **MessageSender** command line executable to send messages to the deployed [!INCLUDE[bridge](/Token/bridge_md.md)]. This tool accepts command line parameters; the sequence and usage of those parameters are:

   ```
   MessageSender.exe <ACSNamespace> <IssuerName> <IssuerKey> <RuntimeAddress> <MessageFilepath> <ContentType>
   ```
   Where:

   |Parameter name <br /> <br />|Description <br /> <br />|
   |------------------|---------------|
   |ACSNamespace <br /> <br />|The Access Control namespace <br /> <br />|
   |IssuerName <br /> <br />|Issuer Name for the above namespace <br /> <br />|
   |IssuerKey <br /> <br />|Issuer Key for the above namespace <br /> <br />|
   |RuntimeAddress <br /> <br />|Runtime address or the endpoint URL where the [!INCLUDE[bridge](/Token/bridge_md.md)] is deployed. You got this address in [Step 6: Build and Deploy the Project](/Topic/Step_6__Build_and_Deploy_the_Project.md). <br /> <br />|
   |MessageFilePath <br /> <br />|Path to the file that contains the request message to be sent to the [!INCLUDE[bridge](/Token/bridge_md.md)]. This request message must be compliant with the **ECommerceSalesOrder.xsd** schema. <br /> <br />You can create an XML instance request message using the request schema you created in [Step 2: Create SalesOrder Schema](/Topic/Step_2__Create_SalesOrder_Schema.md). Alternatively, you can use the SalesOrder.xml sample message available in the sample at [MSDN Code Gallery](http://go.microsoft.com/fwlink/p/?LinkId=316856). <br /> <br />|
   |ContentType <br /> <br />|Determine whether it’s an XML message or an EDI message: <br /> <br /><ul><li>For XML message, set this to **application/xml**. </li><li>For EDI message, set this to **text/plain**. </li> </ul>|

3. For this tutorial, to test the EAI scenario, open a command prompt, go to the solution where you built the **MessageSender** project, and run the following command:

   ```
   MessageSender.exe <ACSNamespace> <IssuerName> <IssuerKey> <endpoint URL of the bridge > <complete path to the request message> "application/xml"
   ```
   This application sends the message to the deployed endpoint and prints the success/failure message.

4. Upon successful completion, the **SalesOrder** table in Northwind’s database has a new sales order entry created.

## See Also
[Create and Deploy the BizTalk Services Project](/Topic/Create_and_Deploy_the_BizTalk_Services_Project.md)

