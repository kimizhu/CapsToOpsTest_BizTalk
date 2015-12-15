---
description: na
keywords: na
pagetitle: Tracking Messages in BizTalk Services portal
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 100d9ba7-0ebc-40bf-8b5f-92641c9639ba
---
# Tracking Messages in BizTalk Services portal
Monitor EDI and AS2 messages, batches, and bridges deployed in a [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. The tracking information helps you in the following ways:

- Determines if a processing delay occurs.

- Provides specific details of a message’s properties.

- Helps determine the flow of events when a message is being processing.

> [!NOTE]
> To track messages processed by the X12 and AS2 pipelines, you must enable tracking as part of an agreement before you can view tracking data. To enable tracking, see [Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md) and [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md).
> 
> To track messages processed by the EAI bridges, you must enable tracking as part of the Visual Studio application. See [Tracking Messages Processed by the Bridge](/Topic/Tracking_Messages_Processed_by_the_Bridge.md). Tracking of messages that failed in processing, is enabled by default. However, to track promoted properties and successfully processed messages, you must explicitly enable tracking while configuring the bridges.

## View and Query Tracked Data
You can view and query tacked data using the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. You can use the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to track messages based on three different criterion – messages, protocol (X12 or AS2), and batching.

#### To view and query tracked data based on messages

1. Select **Tracking** on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page.

2. On the **Tracking** page, select **Messages**.

3. Select the drop-down arrow against the **Search** box to see different fields based on which you can filter the tracking data to be viewed.

   |Parameter <br /> <br />|Description <br /> <br />|
   |-------------|---------------|
   |Request ID <br /> <br />|The request ID of the message sent to the [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
   |Track ID <br /> <br />|The ID received in response to sending a message to an endpoint. The tracking ID is same as the request ID that is sent back to the client. **Note:** By default, the tracking ID you must have received includes a **_Gx** as a suffix, where **&#42;x&#42;** is a numeric number. While looking at tracking information using the tracking ID, you must remove the **_Gx** suffix. <br />|
   |Event Level <br /> <br />|The event category (Error or All) that you want to filter in the tracking data. <br /> <br />|
   |Endpoint URL <br /> <br />|The relative endpoint URL where the endpoint is deployed. <br /> <br />|
   |Date From <br /> <br />|The start date/time from which the tracking data must be retrieved. <br /> <br />|
   |Date To <br /> <br />|The end date/time up to which the tracking data must be retrieved. <br /> <br />|
   > [!NOTE]
   > **Event Level**, **Date From**, and **Date To** are always enabled by default in the search filter. However, **Date From** and **Date To** must be filled according to local time zone. The default **Date To** is the current local time and default **Date From** is the current local time minus 24 hours (1 Day).

4. Click **Search**.

#### To view and query tracked data based on protocol

1. Select **Tracking** on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page.

2. On the **Tracking** page, select **Protocol**, and then select either **X12** or **AS2**.

3. Select the drop-down arrow next to the **Search** box to see different fields based on which you can track the messages.

   |Parameter <br /> <br />|Applicable to <br /> <br />|Description <br /> <br />|
   |-------------|-----------------|---------------|
   |Sender <br /> <br />|X12 and AS2 <br /> <br />|The Sender can be a specific partner or any partner. You can also use **&lt; Any &#42;&gt;** as a wild card. <br /> <br />|
   |Receiver <br /> <br />|X12 and AS2 <br /> <br />|The Receiver can be a specific partner or any partner. You can also use **&lt; Any &#42;&gt;** as a wild card. <br /> <br />|
   |Message Type <br /> <br />|X12 <br /> <br />|The Message Type can be a specific type, like 850–Purchase Order, or any type. You can also use **&lt; Any &#42;&gt;** as a wild card. <br /> <br />|
   |Interchange ID <br /> <br />|X12 <br /> <br />|The interchange ID for the message to be tracked. <br /> <br />|
   |AS2 Message ID <br /> <br />|AS2 <br /> <br />|The AS2 message ID for the message to be tracked <br /> <br />|
   |Request ID <br /> <br />|X12 and AS2 <br /> <br />|The request ID of the message sent to the [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
   |Date From <br /> <br />|X12 and AS2 <br /> <br />|The start date/time after which the tracking data must be retrieved. <br /> <br />|
   |Date To <br /> <br />|X12 and AS2 <br /> <br />|The end date up to which the tracking data must be retrieved. <br /> <br />|
   > [!NOTE]
   > **Date From** and **Date To** are always enabled by default in the search filter. However, values for these filters must be filled according to local time zone. The default value for **Date To** is the current local time and the default value for **Date From** is the current local time minus 24 hours (1 Day).

4. Select **Search**.

   Once you see the filter tracking data, you can also download the messages from the portal. Click the row in the list and then click **Details** from the command bar to get an option to download more data. For example, for an X12 tracking row, you can download the EDI message, suspended message, and the corresponding correlated functional acknowledgements. Similarly, for AS2 tracking row, you can download the AS2 message before encoding/decoding and the corresponding correlated MDNs. This is available only with the [!INCLUDE[af_integration](/Token/af_integration_md.md)] Premium edition.

#### To view and query tracked data based on batching

1. Select **Tracking** on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page.

2. On the **Tracking** page, select **Batching**, and then select either **active batches** or **completed batches**.

3. Select the drop-down arrow against the **Search** box to see different fields based on which you can track the messages.

   |Parameter <br /> <br />|Applicable to <br /> <br />|Description <br /> <br />|
   |-------------|-----------------|---------------|
   |Sender <br /> <br />|Active and completed <br /> <br />|The Sender can be a specific partner or any partner. You can also use **&lt; Any &#42;&gt;** as a wild card. <br /> <br />|
   |Receiver <br /> <br />|Active and completed <br /> <br />|The Receiver can be a specific partner or any partner. You can also use **&lt; Any &#42;&gt;** as a wild card. <br /> <br />|
   |Agreement <br /> <br />|Active and completed <br /> <br />|The name of the agreement containing the batch configuration. You can also use **&lt; Any &#42;&gt;** as a wild card. <br /> <br />|
   |Batch <br /> <br />|Active and completed <br /> <br />|The name of the batch that processes the message. You can also use **&lt; Any &#42;&gt;** as a wild card. <br /> <br />|
   |Request ID <br /> <br />|Completed <br /> <br />|The request ID of the message sent to the [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
   |Completed Time From <br /> <br />|Completed <br /> <br />|The start date after which the batch is released. <br /> <br />|
   |Completed Time To <br /> <br />|Completed <br /> <br />|The end date before which the batch is released. <br /> <br />|
   > [!NOTE]
   > **Completed Time From** and **Completed Time To** are always enabled by default in the search filter. However, you must enter the value for these filters according to local time zone. The default value for **Completed Time To** is the current local time and the default value for **Completed Time From** is the current local time minus 24 hours (1 Day).

4. Click **Search**.

## Known Issue
Tracking events are captured up to the X12/AS2 message processing and correlation of the acknowledgements only in the **Protocol** (**X12** or **AS2**) tracking tabs. If a message fails outside of the Protocol stage, the tracking view still shows the message as successfully processed. In this situation, refer to the **Messages** tab in Tracking for error details. As a tip, you must copy the Request ID from **X12** or **AS2** tracking tab and use that ID as a search filter in the **Messages** tab.

The X12 Receive and Send Settings ([Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md)) provides information on the Protocol stage.

## See Also
[Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md)
[Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md)
[Manage your Resources in BizTalk Services portal](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md)
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)

