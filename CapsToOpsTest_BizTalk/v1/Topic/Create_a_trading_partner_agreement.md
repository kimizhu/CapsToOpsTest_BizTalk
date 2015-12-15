---
description: na
keywords: na
pagetitle: Create a trading partner agreement
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6f3a867-cf2c-47b4-85be-a1ffc2becd68
---
# Create a trading partner agreement
In this section, we create a trading partner agreement between Contoso, Ltd. and the Fourth Coffee restaurant. The trading partner agreement serves as a contract between the two partners. Because Contoso, Ltd. has the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription, Contoso, Ltd. uses the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to create the agreement in the following manner:

- The send side agreement mandates that Contoso, Ltd. sends an X12 850 purchase order to Fourth Coffee.

- The receive side agreement mandates that Fourth Coffee sends an X12 810 invoice back to Contoso, Ltd.

This topic provides instructions on how to create the send and receive side agreements. Before performing these instructions you must have  performed the following steps:

- Registered the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] for your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. For instructions on how to register the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], see [Registering the Portal](http://msdn.microsoft.com/library/windowsazure/hh689837.aspx)

- Created a partner called **FourthCoffee** using the partner onboarding application as described in [Set up the application to onboard partners](/Topic/Set_up_the_application_to_onboard_partners.md)

## Create trading partners
As a first step, create a trading partner that represents Contoso, Ltd.

1. From the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], select the **Partners** tab, and from the command bar, select **Add**.

2. Enter the partner name as **Contoso**, and then from the command bar, select **Save**.

## Create an agreement
For this tutorial, Contoso, Ltd. deploys the agreement between Fourth Coffee and itself. So, Contoso, Ltd. is the “hosting partner” for the agreement. To begin with, create an agreement with Contoso, Ltd. as the hosting partner.

1. From the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], select the **Agreements** tab, select the **X12** tab select **Add** from the command bar.

2. On the New Agreement page, enter **ContosoFourthCoffee** as the agreement name.

3. For the hosted partner, select **Contoso**. The default profile for Contoso is automatically selected.

   For the hosted partner identity, set **Qualifier** to **ZZ-Mutually Defined** and **Value** to **Contoso**.

4. For the guest partner, select **FourthCoffee**.

   For the hosted partner identity, set **Qualifier** to **ZZ-Mutually Defined** and **Value** to **FourthCoffee**.

5. Select the check boxes to track and archive send and receive-side messages and message properties.

6. Select **Continue**. When you do this, two new tabs are added towards the top. These two tabs are used to create the send and receive sides of the agreement.

### Create the send agreement
There are two parts to a trading partner agreement, the send agreement and the receive agreement. The key to understanding the send and receive agreements is to understand who is creating and deploying the agreement. In this tutorial, Contoso, Ltd. is the hosting partner and hence the send side agreement is used to process messages sent from the hosted partner (Contoso) to the guest partner (Fourth Coffee). For this tutorial, the send side agreement ensures that an X12 850 purchase order is processed and routed from Contoso, Ltd. to Fourth Coffee.

According to the application flow described in [Implementing the Business Scenario](/Topic/Using_BizTalk_Services_from_a_Windows_8_Application.md#BKMK_Scenario), the purchase order message (after it is processed by the EDI send bridge) is routed to an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob from where the Fourth Coffee restaurant consumes the message. So, before performing the steps provided here, make sure you have a blob container created in [!INCLUDE[azure_2](/Token/azure_2_md.md)]. In the step [Create Azure blob containers](/Topic/Create_Azure_blob_containers.md), you already created a blob container (**tosupplier**) for the same purpose.

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], for the **ContosoFourthCoffee** agreement, select the **Send Settings** tab.

2. For the **Inbound URL** view, the read-only **Endpoint** field displays the URL where the purchase order is received and then processed by the EDI bridge, before being routed to the **tosupplier**[!INCLUDE[azure_2](/Token/azure_2_md.md)] blob.

3. For **Transform** view, you don’t need to upload any transforms because the purchase order message received by the EDI bridge is already transformed into the right 850 format by the EAI bridge you configured in the step [Add an XML one-way bridge to process purchase order](/Topic/Add_an_XML_one-way_bridge_to_process_purchase_order.md).

4. For the **Batching** view again, you don’t need to make any changes because you want the messages to be sent to Fourth Coffee restaurant as and when they are received.

5. For the **Protocol** view, select the **TA1 expected** and **997 expected** check boxes if you want to receive technical and functional acknowledgements.

   Under the **Schemas** section, upload the schema of the X12 850 purchase order message. You included the schema (X12_00401_850.xsd) in the **CloudCar_Integration_PurchaseOrder** project you created earlier. Provide the following values:

   |||
   |-|-|
   |Version <br /> <br />|00401 <br /> <br />|
   |Transaction Type (ST01) <br /> <br />|850 – Purchase Order <br /> <br />|
   |Schema <br /> <br />|/X12_00401_850.xsd <br /> <br />|

6. For the **Transport** view, enter the [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob container you created earlier where the message will be routed. Also, enter an endpoint where any messages that fail during processing are routed.

   - Under the **Transport settings** section, do the following:

      1. For **Transport type**, select **Azure Blobs**.

      2. Enter the shared access signature URL for the **tosupplier** container in [!INCLUDE[azure_2](/Token/azure_2_md.md)] Blob storage where the messages are routed to. For instructions on how to generate the SAS, see [Create and Use a Shared Access Signature](http://msdn.microsoft.com/library/windowsazure/jj721951.aspx). You can also use the Azure Storage Explorer to generate SAS. For more information about the Azure Storage Explorer, see [Azure Storage Explorer](http://go.microsoft.com/fwlink/p/?LinkID=282292).

   - Under the **Message Suspension Settings** section, enter a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint where all failed messages are routed. Do the following:

      1. For **Transport type**, select **Azure Service Bus**.

      2. For **Route Destination Type**, select **BasicHttpRelay**, and enter the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace, issuer name, and issuer key.

      3. Enter the relay endpoint as **failedmessages**. So, the URL at which the failed messages are routed to will be `https://*<servicebus_namespace>*.servicebus.windows.net/failedmessages`.

   ![](/Image/WABS_CloudCar_Send_Transport.png)

With this, you complete the configuration of the send-side agreement.

### Create the receive agreement
The receive-side agreement is used to process messages received by the hosted partner. For this tutorial, the receive-side agreement ensures that an X12 810 invoice is processed and routed from Fourth Coffee to Contoso, Ltd.

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], for the **ContosoFourthCoffee** agreement, select the **Receive Settings** tab.

2. For the **Transport** view, the read-only **Endpoint** field displays the URL where the invoice (sent by Fourth Coffee) is received.

3. For the **Protocol** view, select the **TA1 expected** and **997 expected** check boxes if you want to receive technical and functional acknowledgements.

   Under the **Schemas** section, upload the schema of the X12 810 invoice message. You included the schema (X12_00401_810.xsd) in the **CloudCar_Integration_Invoice** project you created earlier. Provide the following values:

   |||
   |-|-|
   |Version <br /> <br />|00401 <br /> <br />|
   |Transaction Type (ST01) <br /> <br />|810 – Invoice <br /> <br />|
   |Sender Application (GS02) <br /> <br />|FROM-SUPPLIER <br /> <br />|
   |Schema <br /> <br />|/X12_00401_850.xsd <br /> <br />|

4. For **Transform** view, you don’t need to upload any transforms because the invoice message is routed to the EAI bridge, as-is. The EAI bridge you configured in the step [Add an XML one-way bridge to process invoice](/Topic/Add_an_XML_one-way_bridge_to_process_invoice.md) transforms the message before routing it to a blob store.

5. In the **Route** view, enter how and where the messages are routed.

   - The **Route Settings** section governs how and where the successfully-processed messages are routed.

      1. Under **Route Settings**, select **Add**, and then enter a name for the routing rule

      2. Because we are routing all messages received by the EDI receive bridge to the EAI bridge, we don’t need to set a route rule. The default rule is to forward all messages to the destination endpoint.

      3. We are not adding any properties to the message body or header, so we don’t need to enter any route action as well.

      4. Under **Route destination**, for **Transport type**, select **Azure BizTalk Bridge** and enter the relative address of the EAI bridge you created earlier for processing invoices. In the step [Add an XML one-way bridge to process invoice](/Topic/Add_an_XML_one-way_bridge_to_process_invoice.md), you entered the bridge address as **InvoiceBridge**, so enter the same value here.

      5. Select **Save**.

   - Under the **Message Suspension Settings** section, enter a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint where all failed messages are routed. Do the following:

      1. For **Transport type**, select **Azure Service Bus**.

      2. For **Route Destination Type**, select **BasicHttpRelay**, and select the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace, issuer name, and issuer key.

      3. Enter the relay endpoint as **failedmessages**. The URL to which failed messages are is `https://*<servicebus_namespace>*.servicebus.windows.net/failedmessages`.

   ![](/Image/WABS_CloudCar_Rcv_Transport.png)

6. Select **Deploy** to deploy the agreement. One your agreement is deployed, the endpoints for the receive-side and send-side EDI bridges will be in the following format:

   - **Receive side** –`https://*<mybiztalkservice>*.biztalk.windows.net/default/Agreements/*<id>*/Receive`

   - **Send side** –`https://*<mybiztalkservice>*.biztalk.windows.net/default/Agreements/*<id>*/Send`

   These endpoint URLs are available from the **Receive Settings** tab (Transport view) and **Send Settings** tab (Inbound URL view) of the deployed agreement.

## See Also
[Set up the integration layer](/Topic/Set_up_the_integration_layer.md)

