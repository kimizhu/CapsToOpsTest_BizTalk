---
description: na
keywords: na
pagetitle: Tracking Messages Processed by the Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04a41fee-5705-43d1-8ee3-2b78e130a3ac
---
# Tracking Messages Processed by the Bridge
Within a bridge, a message undergoes processing under various stages and can be routed to configured endpoints. Specific details of the message (like transport properties, message properties, and so on) need to be tracked and queried separately by the bridge developers to keep a track of message processing. Additionally, while a message is being processed by the bridge, there can be failures of many types. These failures must be propagated back to the bridge developers/administrators or the message-sending client so that appropriate actions can be taken to fix these errors.

Bridges provide support for tracking the messages thereby enabling the bridge developer and message sending clients to track message properties defined during the bridge configuration. You can configure the bridge to track the messages using options available from the [!INCLUDE[msgflow](/Token/msgflow_md.md)] surface.

In this topic:

[How Tracking Works?](/Topic/Tracking_Messages_Processed_by_the_Bridge.md#BKMK_HowItWorks)

[How to View Tracked Properties?](/Topic/Tracking_Messages_Processed_by_the_Bridge.md#BKMK_HowToView)

[Configure Tracking](/Topic/Tracking_Messages_Processed_by_the_Bridge.md#BKMK_ConfigureTracking)

## <a name="BKMK_HowItWorks"></a>How Tracking Works?
There are two parts to tracking a message – what gets tracked and when it gets tracked. Through the bridge configuration, you can define (to some extent) what properties get tracked. Properties specific to the FTP source (if available as part of a message flow) are always tracked and can’t be opted out. When these properties get tracked depends on certain events that are transparent to the user. These events, in turn, depend on what stage of the bridge the message is at. For example:

The following list details “what” can be tracked:

- **X_PIPELINE_MESSAGE TYPE** and **X_PIPELINE_REQUESTMESSAGETYPE** properties. These properties are always promoted on a message processed by the bridge.

- All properties that are promoted at the **Enrich** stage of a bridge.

- If a message flow includes an FTP source, the following FTP-specific data is also tracked:

   - Source name (name of the FTP source on the itinerary designer)

   - When an FTP source is started/stopped.

   - Filename

   - FTP server

   - FTP folder path

   - FTP username

The following list details “when” these properties get tracked:

1. Even when you do not select any properties to be tracked, the following events are always tracked:

   - Activity faulted (for all activities)

   - Stage faulted (for all stages)

   - Pipeline faulted

   - Route destination

2. When you select the properties to be tracked, the following events are tracked:

   - All events in bullet 1 along with selected message properties

   - Route stage started along with selected message properties

   - SendReply stage started along with selected message properties

3. When you opt to track message processing events, the following events are tracked:

   - All events in bullet 1 along with selected message properties

   - Pipeline started/completed

   - Artifact retrieved/not found

## <a name="BKMK_HowToView"></a>How to View Tracked Properties?
You can view the tracking data from the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. See [Tracking Messages in BizTalk Services portal](/Topic/Tracking_Messages_in_BizTalk_Services_portal.md).

## <a name="BKMK_ConfigureTracking"></a>Configure Tracking

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], as described in [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. From the **Toolbox**, drag and drop a bridge component ([!INCLUDE[one-way](/Token/one-way_md.md)], [!INCLUDE[request_response](/Token/request_response_md.md)], or [!INCLUDE[passthru](/Token/passthru_md.md)]) to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface.

3. Right-click the bridge component that you added, and in the **Properties** window click the ellipsis **(…)** against **Track Properties**.

4. In the **Track Properties** dialog box, do the following:

   1. Select the **Track message processing events** check box to track detailed information such as when a stage starts, completes, or faults; when an activity within a stage starts, completes, or faults; whether an artifact gets retrieved, etc.

   2. Select the **Track all message properties** check box to track all the message properties. If you promoted any properties within the bridge Enrich stages, those properties are also tracked along with default properties – **XPIPELINE_MESSAGETYPE** and **XPIPELINE_REQUESTMESSAGETYPE**. The default properties are implicitly promoted by the bridge itself.

      - OR -

      Select the specific properties that you want to track.

   3. Click **OK**.

      You can view the tracking data in the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal. For more information, see [Tracking Messages in BizTalk Services portal](/Topic/Tracking_Messages_in_BizTalk_Services_portal.md).

The following table describes how the selections you make in the **Track Properties** dialog box change what gets tracked:

|Selection <br /> <br />|What Gets Tracked <br /> <br />|
|-------------|---------------------|
|No selection <br /> <br />|Even if you do not select any options in the dialog box, the pipeline state, the stage state, whether the route destinations are successfully ascertained, and the activity state are tracked for any message processing faults. This means that by default, any faults in any of the stages or activities will get tracked. <br /> <br />|
|When **Track all message properties** or specific properties are selected <br /> <br />|The properties you selected are tracked as part of the faulted event for a pipeline state, the stage state, or the activity state. This means that if you select this option, every time there is a fault in the message processing, the values of the selected properties are captured as part of the tracked data. <br /> <br />Over and above this, the properties are also tracked before the Route Action (routing the message to the intended receiver) and the Reply Action (sending the response back the message sender). <br /> <br />|
|When **Track message processing events** is selected <br /> <br />|The pipeline state, the stage state, or the activity state. Over and above this, the following is also tracked: <br /> <br /><ul><li>When a pipeline state starts and completes </li><li>When an artifact is either successfully retrieved or can’t be retrieved </li> </ul>|

## See Also
[Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md)

