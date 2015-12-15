---
description: na
keywords: na
pagetitle: Step 4: Test the EDI Solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 43e665ec-ae3d-4e1e-b810-61cff6f292bf
---
# Step 4: Test the EDI Solution
In this step, we test the EDI solution by sending a message to the endpoint where the EDI receive [!INCLUDE[bridge](/Token/bridge_md.md)] is deployed. You can send messages to the endpoint both in HTTP or SOAP protocols. The instructions below demonstrate how to send the message via HTTP.

### To test the EDI solution

1. Download the **MessageSender** tool from [Azure BizTalk Services Samples](http://go.microsoft.com/fwlink/?LinkId=303933).

2. Build the project and use the resulting **MessageSender** command line executable to send messages to the deployed [!INCLUDE[bridge](/Token/bridge_md.md)] endpoint. This tool accepts command line parameter, and the sequence and usage of those parameters is given below:

   ```
   MessageSender.exe <ACSNamespace> <IssuerName> <IssuerKey> <RuntimeAddress> <MessageFilepath> <ContentType>
   ```
   Where,

   TABLE REMOVED

3. For this tutorial, to test the EDI scenario, open a command prompt, navigate to the solution where you built the **MessageSender** project, and run the following command:

   ```
   MessageSender.exe <ACSNamespace> <IssuerName> <IssuerKey> <endpoint URL of the agreement> <complete path to the request message> "text/plain"
   ```
   This application sends the message to the deployed endpoint and prints the success/failure message.

4. Upon successful completion, the **SalesOrder** table in Northwind’s database must have a new sales order entry created.

5. Because you chose to receive acknowledgements, you get those acknowledgements on the endpoint you specified as part of the EDI send settings. For example, for successfully processed acknowledgements, you specified the endpoint as `http://*servicebus namespace*.servicebus.windows.net/Success`.  You can use the **MessageReceiver** tool to receive those acknowledgements.

   1. Download the **MessageReceiver** tool from [Azure BizTalk Services Samples](http://go.microsoft.com/fwlink/?LinkId=303933).

   2. Build the project and use the resulting command line executable to receive messages at a [!INCLUDE[sb2](/Token/sb2_md.md)] endpoint. This tool accepts command line parameter, and the sequence and usage of those parameters is given below:

      ```
      MessageReceiver.exe <ServiceBusNamespace> <IssuerName> <IssuerKey> <RelativeAddress> <Mode>
      ```
      Where,

      |Parameter name <br /> <br />|Description <br /> <br />|
      |------------------|---------------|
      |[!INCLUDE[sb2](/Token/sb2_md.md)] Namespace <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|
      |IssuerName <br /> <br />|Issuer Name for the above namespace <br /> <br />|
      |IssuerKey <br /> <br />|Issuer Key for the above namespace <br /> <br />|
      |RelativeAddress <br /> <br />|Relative address for the entity to be hosted. You get this address from the **Transport** page of the **Send Settings** tab for the agreement you created in [Step 3: Create Agreements Between Partner Profiles](/Topic/Step_3__Create_Agreements_Between_Partner_Profiles.md). <br /> <br />For this tutorial, you configured the agreement to send successfully processed acknowledgements to `http://*servicebus namespace*.servicebus.windows.net/Success`, so you must set this parameter to **Success**. <br /> <br />|
      |Mode <br /> <br />|Indicate whether the entity is a Queue, one-way relay, or a two-way relay. For this tutorial, because we chose to receive the messages to a one-way relay, you must set this to **OneWayRelay**. <br /> <br />|
      For this tutorial, to test the EDI solution, open a command prompt, navigate to the solution where you built the MessageReceiver project, and run the following command:

      ```
      MessageReceiver.exe <ServiceBusNamespace> <IssuerName> <IssuerKey> Success OneWayRelay
      ```
      This console application shows the message received at the endpoint. The message is also saved under the \bin\Debug folder of the **MessageReceiver** project.

      > [!NOTE]
      > You can run another instance of the MessageReceiver tool to receive messages that are sent to the failure endpoint, which you configured in the agreement as `http://*servicebus namespace*.servicebus.windows.net/Failure`.

6. Because you enabled tracking as part of the agreement, you can also see the message tracking data as the message is processed by the EDI pipeline. To view the tracking data, on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Tracking**.

## See Also
[Create and Deploy the Trading Partner Agreement](/Topic/Create_and_Deploy_the_Trading_Partner_Agreement.md)

