---
description: na
keywords: na
pagetitle: Step 6: Test the Solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.service: multiple
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0b7c696-df2d-4c1a-95de-1369b8557eef
---
# Step 6: Test the Solution
In this topic, you go through the procedures to test the solution. This solution has two scenarios to be tested:

- **The success scenario** where the message is routed from the EDI receive pipeline to the intermediary [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)], hosted at `https://*<mybiztalkservicename>*.biztalk.windows.net/default/B2BConnector`, which finally routes the message to an on-premise SAP Server via a relay endpoint hosted on [!INCLUDE[sb2](/Token/sb2_md.md)]. To test this scenario, you drop a valid X12 850 PO message to the FTP location and then use the SAP GUI to see if the ORDERS05 IDOC is received in SAP.

- **The failure scenario** where the message is routed to `https://*<servicebus_namespace>*.servicebus.windows.net/Suspend`. To test this scenario, we’ll drop an invalid X12 850 PO message (so that it fails), and gets routed to failure endpoint. We use a relay receiver service that captures any message that hits the failure endpoint and writes the error message to an XML file.

### To test the success scenario

1. Navigate to the location where you downloaded and extracted **SAPIntegration.zip**. From the **InputMessages** folder, copy **Success_SampleMessage.edi** and drop it to the FTP location you specified in the EDI agreement. Wait for the file to disappear.

2. Using the SAP GUI, logon to the SAP Server you are targeting for this scenario. On the home screen, enter **WE02** in the text box and press **ENTER**:

   ![](/Image/AFINT_PG_SAP1.gif)

3. On the IDOC List page, press **F8** to retrieve a list of IDOCs received. You must see an entry for the most recent IDOC received, as shown in the following screenshot:

   ![](/Image/AFINT_PG_SAP_IDOCRcvd.gif)

### To test the failure scenario

1. Download the **MessageReceiver** tool from [Azure BizTalk Services Samples](http://go.microsoft.com/fwlink/p/?LinkId=303933).

2. Build the project and use the resulting command line executable to receive messages at a [!INCLUDE[sb2](/Token/sb2_md.md)] endpoint. This tool accepts command line parameter, and the sequence and usage of those parameters are:

   ```
   MessageReceiver.exe <ServiceBusNamespace> <IssuerName> <IssuerKey> <RelativeAddress> <Mode>
   ```
   Where:::

   |Parameter name <br /> <br />|Description <br /> <br />|
   |------------------|---------------|
   |[!INCLUDE[sb2](/Token/sb2_md.md)] Namespace <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|
   |IssuerName <br /> <br />|Issuer Name for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|
   |IssuerKey <br /> <br />|Issuer Key for the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|
   |RelativeAddress <br /> <br />|Relative address of the relay endpoint where suspended messages are routed. You get this address under the **Message Suspension Settings** section of the **Route** page on the **Receive Settings** tab for the agreement you created in [Step 5: Create and Deploy the EDI Receive Pipeline](/Topic/Step_5__Create_and_Deploy_the_EDI_Receive_Pipeline.md). <br /> <br />For this tutorial, you configured the agreement to send suspended messages to `http://*<servicebus_namespace>*.servicebus.windows.net/Suspend`, so you must set this parameter to **Suspend**. <br /> <br />|
   |Mode <br /> <br />|Indicate whether the entity is a Queue, one-way relay, or a two-way relay. For this tutorial, because we chose to receive the messages to a one-way relay, you must set this to **OneWayRelay**. <br /> <br />|
   For this tutorial, to test the EDI solution, open a command prompt, navigate to the solution where you built the MessageReceiver project, and run the following command:

   ```
   MessageReceiver.exe <ServiceBusNamespace> <IssuerName> <IssuerKey> Suspend OneWayRelay
   ```
   This starts the relay service where the suspended messages get routed to.

3. Navigate to the location where you downloaded and extracted **SAPIntegration.zip**. From the **InputMessages** folder, copy **Failure_SampleMessage.edi** and drop it to the FTP location you specified in the EDI agreement. Wait for the file to disappear.

4. Switch back to the **MessageReceiver** console window. This console application shows the message received at the endpoint. The message is also saved under the \bin\Debug folder of the **MessageReceiver** project.

## See Also
[Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server](/Topic/Tutorial__Using_Azure_BizTalk_Services_to_Integrate_with_an_On-Premises_SAP_Server.md)

