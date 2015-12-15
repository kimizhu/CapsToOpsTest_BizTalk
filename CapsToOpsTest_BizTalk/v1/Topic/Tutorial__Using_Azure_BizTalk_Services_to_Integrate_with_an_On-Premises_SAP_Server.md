---
description: na
keywords: na
pagetitle: Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.service: multiple
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eeafa523-a79d-48e0-9ae0-c91d5b87a721
---
# Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server
[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] provides a rich set of integration capabilities enabling organizations to create hybrid solutions such that their customer or partner facing applications are hosted on Azure, while the data related to customers or partners is stored on-premises using LOB applications. In this article, we talk about how to set up a similar hybrid scenario using [!INCLUDE[af_integration](/Token/af_integration_md.md)]. To demonstrate how to integrate [!INCLUDE[azure_1](/Token/azure_1_md.md)] applications with an on-premises LOB application using [!INCLUDE[af_integration](/Token/af_integration_md.md)], let us consider a scenario involving two business partners: Fabrikam and Contoso.

## Business Scenario
Contoso sends a purchase order (PO) message to Fabrikam in an X12 Electronic Data Interchange (EDI) format using the PO (**X12 850**) schema. Fabrikam (that uses an SAP Server to manage partner data) accepts PO from its partners using the **ORDERS05** IDOCS. To enable Contoso to send a PO directly to Fabrikam’s on-premises SAP Server, Fabrikam decides to use [!INCLUDE[af_integration](/Token/af_integration_md.md)] to set up a hybrid integration scenario where the integration layer is hosted on [!INCLUDE[azure_2](/Token/azure_2_md.md)] and the SAP Server is within the organization’s firewall. Fabrikam uses [!INCLUDE[af_integration](/Token/af_integration_md.md)] in the following ways to enable this hybrid integration scenario:

1. Fabrikam uses [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK to create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. The project includes a [!INCLUDE[one-way](/Token/one-way_md.md)] to send messages to a relay endpoint, which in turns sends the message to the on-premises SAP system.

2. Fabrikam uses the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] component available with [!INCLUDE[af_integration](/Token/af_integration_md.md)] to expose the **Send** operation on ORDERS05 IDOC as an operation using [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint. The [!INCLUDE[one-way](/Token/one-way_md.md)] sends messages to this relay endpoint. Fabrikam also creates the schema for **Send** operation using [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] and includes the schema as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

   > [!NOTE]
   > A **Send** operation on an IDOC is an operation that is exposed by the [!INCLUDE[bap](/Token/bap_md.md)] on any IDOC to send the IDOC to the SAP Server. [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] uses BizTalk Adapter Pack to connect to an SAP Server.

3. Fabrikam uses the [!INCLUDE[transform](/Token/transform_md.md)] component available with [!INCLUDE[af_integration](/Token/af_integration_md.md)] to create a map to transform the PO message in X12 format into the schema required by the SAP Server to invoke the **Send** operation on the ORDERS05 IDOC.

4. Fabrikam uses the [!INCLUDE[tpm_full](/Token/tpm_full_md.md)] available with [!INCLUDE[af_integration](/Token/af_integration_md.md)] to create and deploy an EDI agreement under the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription that processes the X12 850 PO message. As part of the message processing, the agreement also does the following:

   1. Receives an X12 850 PO message over FTP.

   2. Transforms the X12 PO message into the schema required by the SAP Server using the transform created earlier.

   3. Routes the transformed message to the [!INCLUDE[one-way](/Token/one-way_md.md)] that eventually routes the message to a relay endpoint created for sending a PO message to an SAP Server. Fabrikam earlier exposed (as explained in bullet 1 above) the Send operation on ORDERS05 IDOC as a relay endpoint, to enable partners to send PO messages using [!INCLUDE[lobconnect](/Token/lobconnect_md.md)].

Once this is set up, Contoso drops an X12 850 PO message to the FTP location. This message is consumed by the EDI receive pipeline, which processes the message, transforms it to an ORDERS05 IDOC, and routes it to the intermediary [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]. The [!INCLUDE[bridge](/Token/bridge_md.md)] then routes the message to the relay endpoint on [!INCLUDE[sb2](/Token/sb2_md.md)], which is then sent to the on-premises SAP Server. The following illustration represents the same scenario.

![](/Image/AFINT_PG_Scenario.gif)

## How to Use This Article
This tutorial is written around the **SAPIntegration** sample available from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=241990) (**SAPIntegration.zip**). You could either use the **SAPIntegration** sample and go through this tutorial to understand how the sample was built or just use this tutorial to create your own application. This tutorial is targeted towards the second approach so that you get to understand how this application was built. Also, to be consistent with the sample, the names of artifacts (e.g. schemas, transforms, etc.) used in this tutorial are same as that in the sample.

The sample available from the MSDN code gallery contains only half the solution, which can be developed at design-time on your computer. The sample cannot include the configuration that you must do on the [!INCLUDE[azure_2](/Token/azure_2_md.md)][!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. For that, you must follow the steps in this tutorial to set up your EDI [!INCLUDE[bridge](/Token/bridge_md.md)]. Even though Microsoft recommends that you follow the tutorial to best understand the concepts and procedures. If you really wish to use the sample, this is what you should do:

- Download the **SAPIntegration.zip** package, extract the **SAPIntegration** sample, and make relevant changes like adding your service namespace, issuer name, issuer key, SAP Server details, and so on. After changing the sample, deploy the application to get the endpoint URL at which the [!INCLUDE[one-way](/Token/one-way_md.md)] is deployed.

- Use the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to configure the Receive settings as described at [Step 5: Create and Deploy the EDI Receive Pipeline](/Topic/Step_5__Create_and_Deploy_the_EDI_Receive_Pipeline.md) and follow the procedures to route messages from the EDI Receive [!INCLUDE[bridge](/Token/bridge_md.md)] to the [!INCLUDE[one-way](/Token/one-way_md.md)] you already deployed.

- Drop a test message at the FTP location configured as part of the agreement and verify that the application works as expected.

   - If the message is successfully processed, it is routed to the SAP Server and you can verify the ORDERS IDOC using the SAP GUI.

   - If the EDI agreement fails to process the message, the failure/error messages are routed to a relay endpoint on [!INCLUDE[sb2](/Token/sb2_md.md)]. To receive such messages, you must set up a relay receiver service that receives any message that comes to that specific relay endpoint.  More details on why you need this service and how to use it are available at [Step 6: Test the Solution](/Topic/Step_6__Test_the_Solution.md).

## In This Section

- [Step 1: Get yYour Computer Ready](/Topic/Step_1__Get_yYour_Computer_Ready.md)

- [Step 2: Expose a Relay Endpoint to Invoke Operations on ORDERS05 IDOC](/Topic/Step_2__Expose_a_Relay_Endpoint_to_Invoke_Operations_on_ORDERS05_IDOC.md)

- [Step 3: Transform the X12 850 PO Message to the ORDERS05 Message](/Topic/Step_3__Transform_the_X12_850_PO_Message_to_the_ORDERS05_Message.md)

- [Step 4: Create and Deploy the XML Bridge](/Topic/Step_4__Create_and_Deploy_the_XML_Bridge.md)

- [Step 5: Create and Deploy the EDI Receive Pipeline](/Topic/Step_5__Create_and_Deploy_the_EDI_Receive_Pipeline.md)

- [Step 6: Test the Solution](/Topic/Step_6__Test_the_Solution.md)

## See Also
[Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server](/Topic/Tutorial__Using_Azure_BizTalk_Services_to_Integrate_with_an_On-Premises_SAP_Server.md)

