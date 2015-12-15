---
description: na
keywords: na
pagetitle: Create a Pass-Through Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e78d4649-c4ed-4adb-b34f-23b51a4c1d8b
---
# Create a Pass-Through Bridge
Create a [!INCLUDE[passthru](/Token/passthru_md.md)] as part of a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

A [!INCLUDE[passthru](/Token/passthru_md.md)] has only one stage, the **Enrich** stage. This section provides instruction on how to configure each of these stages. Typically, the steps to configure a [!INCLUDE[passthru](/Token/passthru_md.md)] are:

- Add a [!INCLUDE[passthru](/Token/passthru_md.md)] to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

- Configure the Enrich stage of the [!INCLUDE[passthru](/Token/passthru_md.md)].

### To add a [!INCLUDE[passthru](/Token/passthru_md.md)] to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], as described in [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **[!INCLUDE[passthru](/Token/passthru_md.md)]** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area. This adds a *.BridgeConfig* file to the solution.

4. Right-click the [!INCLUDE[passthru](/Token/passthru_md.md)] component, select **Properties**, and then enter the following properties:

   |Property Name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |**Associated Project Item** <br /> <br />|The name of the associated .BridgeConfig file. This is a read-only field, which means that you cannot edit this property to change the name of the .BridgeConfig file. To change the name of the file, you must change the entity name, as defined for the next property, **Entity Name**. <br /> <br />|
   |**Entity Name** <br /> <br />|The name of the [!INCLUDE[passthru](/Token/passthru_md.md)] component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area. This name should be unique for a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. The name of the *.BridgeConfig* file is the same as the entity name you enter here. <br /> <br />|
   |**Relative Address** <br /> <br />|The relative address where the [!INCLUDE[passthru](/Token/passthru_md.md)] is hosted on [!INCLUDE[azure_1](/Token/azure_1_md.md)]. This address along with the [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL you entered in Step 2 is used to create the complete URL for the [!INCLUDE[bridge](/Token/bridge_md.md)]. <br /> <br />For example, if the [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL is **MyBizTalkService** and the relative address of the [!INCLUDE[bridge](/Token/bridge_md.md)] is **PassThruBridge**, the URL for the endpoint on the [!INCLUDE[sb2](/Token/sb2_md.md)] is *https://MyBizTalkService.biztalk.windows.net/default/PassThruBridge*. <br /> <br />|
   |**Route Ordering Table** <br /> <br />|Specifies the routing order of the message from the [!INCLUDE[passthru](/Token/passthru_md.md)] to other components of the message flow. For more information, see [The Routing Order](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_Order). <br /> <br />|
   |**Runtime Address** <br /> <br />|The public runtime endpoint URL where the bridge is deployed. <br /> <br />|
   |**Track Properties** <br /> <br />|You can set this property to define which properties on the message are tracked by the bridge. For instructions on how to set this property, see [Tracking Messages Processed by the Bridge](/Topic/Tracking_Messages_Processed_by_the_Bridge.md). <br /> <br />|

5. Click **Save**.

## Configure the Enrich Stage
The **Enrich** stage enables message enrichment by defining properties, the values for which can be derived from the message header (standard or custom), from system-promoted properties (default properties promoted by the [!INCLUDE[bridge](/Token/bridge_md.md)]), or from an external data source (only [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] tables supported in this release). These properties can then be used to either route the message to a destination endpoint or for further processing by the message receiving entity. In this section, we go through the procedures for performing each of these actions, namely:

- Assigning message header values to properties

- Using system-promoted properties

- Looking up an external data source

#### To configure the Enrich stage

1. Double-click the [!INCLUDE[passthru](/Token/passthru_md.md)] component to open the itinerary designer.

2. Select the **Enrich** stage, and from the **Properties** pane, set the **IsEnabled** property to **True** or **False**.

3. If you want to include any custom code that must be executed before the message enters the **Enrich** stage, set the **On Enter Inspector** property. Similarly, if you want to include any custom code that must be executed after the message exits the **Enrich** stage, set the **On Exit Inspector** property. For more information, on how to set these properties, see [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

4. Within the **Enrich** stage, select the **Enrich** activity, and then from the **Properties** pane click the ellipsis button **(…)** next to the **Property Definition** property to open the **Property Definitions** window.

## See Also
[Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md)

