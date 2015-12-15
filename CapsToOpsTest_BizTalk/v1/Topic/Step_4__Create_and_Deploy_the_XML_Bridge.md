---
description: na
keywords: na
pagetitle: Step 4: Create and Deploy the XML Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.service: multiple
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 83898535-82c4-4e7e-abe9-d07b7ea6558d
---
# Step 4: Create and Deploy the XML Bridge
In this topic, you create an [!INCLUDE[one-way](/Token/one-way_md.md)] that acts as a connector between the EDI Receive [!INCLUDE[bridge](/Token/bridge_md.md)] and the relay endpoint for the ORDERS05 IDOC in SAP. After configuring the [!INCLUDE[bridge](/Token/bridge_md.md)], you connect it to the SAP relay endpoint, and then deploy the solution.

### To configure the XML Bridge

1. In the **SAPIntegration** project, from the Solution Explorer, double-click the **MessageFlowItinerary.bcs** file to open the [!INCLUDE[bridge](/Token/bridge_md.md)] design area.

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**, and update the **BizTalk Service URL** property to include your [!INCLUDE[af_integration](/Token/af_integration_md.md)] name. This is the name that you provided in [Azure classic portal](http://go.microsoft.com/fwlink/?LinkId=517414) while provisioning the [!INCLUDE[af_integration](/Token/af_integration_md.md)].

3. From the **Toolbox**, drag and drop the **[!INCLUDE[one-way](/Token/one-way_md.md)]** component to the bridge design area.

4. Right-click the **[!INCLUDE[one-way](/Token/one-way_md.md)]**, select **Properties**, and change the value for **Entity Name** and **Relative Address** properties to **B2BConnector**. As a result, the complete endpoint URL where the bridge is deployed, which is shown in the **Runtime Address** property, will resemble `https://*<mybiztalkservicename>*.biztalk.windows.net/default/B2BConnector`. This is where the EDI Receive [!INCLUDE[bridge](/Token/bridge_md.md)] sends the ORDERS05 PO message.

5. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] to open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design area. Because this [!INCLUDE[bridge](/Token/bridge_md.md)] only routes the message from the EDI Receive [!INCLUDE[bridge](/Token/bridge_md.md)] to the relay endpoint, there’s not much configuration required for each stage in the [!INCLUDE[bridge](/Token/bridge_md.md)] stage other than specifying the message types of the message that this [!INCLUDE[bridge](/Token/bridge_md.md)] routes. To specify the message type, on the [!INCLUDE[one-way](/Token/one-way_md.md)] design surface, within the **Message Types** box, select the add icon [ ![](/Image/IntSvcs_Bridges_Add_Icon.gif) ] to open the **Message Type Picker** dialog box.

6. In **Message Type Picker**, from the **Available message types** box, select the schema for the request message and then select the right arrow icon  [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ], and then select **OK**. For this tutorial, select the Send schema (`http://Microsoft.LobServices.Sap/2007/03/Idoc/3/ORDERS05//700/Send`). The selected schema is listed under the **Request Message Type** box.

7. Save the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

### To connect the bridge to the relay endpoint

1. In the **SAPIntegration** project, from the **Toolbox**, select the **Connection** component, and connect the [!INCLUDE[one-way](/Token/one-way_md.md)] component with the SAP relay endpoint you already added in [Step 2: Expose a Relay Endpoint to Invoke Operations on ORDERS05 IDOC](/Topic/Step_2__Expose_a_Relay_Endpoint_to_Invoke_Operations_on_ORDERS05_IDOC.md).

2. Set the filter condition on the connection. The routing condition for this scenario is to route all messages to the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. To do so, select the connecting line, and from the **Properties** grid, select the ellipsis **(…)** in the **Filter Condition** property, and then select **Match All**. This ensures that all messages that come to the bridge are routed to the relay endpoint.

3. Set the **Route Action** property on the connection. Before you set the route action, we must understand why it is required. The message sent from the EDI receive [!INCLUDE[bridge](/Token/bridge_md.md)] to the relay endpoint must have the **Action** SOAP header set on it. This header defines what operation must be performed on the SAP system. The message that comes from the EDI receive pipeline does not have this header set. Hence, in this intermediary [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)], you set the route action on the message before it is sent the relay endpoint. As part of the route action, you add the required header on the message. Perform the following steps to set the route action.

   1. Find out the value that will be set for the **Action** SOAP header message. To do so, right-click the SAP relay endpoint from the Server explorer, and from the **Properties** grid, expand **Operations**, and copy the value. For this tutorial, the value is `http://Microsoft.LobServices.Sap/2007/03/Idoc/3/ORDERS05//700/Send`:

      ![](/Image/AFINT_PG_FindAction.gif)

   2. Go back to the [!INCLUDE[bridge](/Token/bridge_md.md)] design area, select the connection between the [!INCLUDE[bridge](/Token/bridge_md.md)] and the SAP relay, and from the **Properties** grid, select the ellipsis **(…)** in the **Route Action** property. In the **Route Actions** dialog box, select **Add** to open the **Add Route Action** dialog box. In **Add Route Action**:

      - Under **Property (Read From)** section, select **Expression** and specify the value that you copied earlier.

         > [!IMPORTANT]
         > Make sure you specify the value for **Expression** within single quotes.

      - Under **Destination (Write-To)** section, set the **Type** to **SOAP** and the **Identifier** to **Action**:

         ![](/Image/AFINT_PG_SetRouteAction.gif)

      - Select **OK** in the **Add Route Action** dialog box to add the route action. Select **OK** in the **Route Actions** dialog box and then select **Save** to save changes to an Enterprise Application Integration project.

4. Save the project. The final bridge configuration resembles the following:

   ![](/Image/AFINT_PG_Bridge.gif)

### To deploy the solution

1. In Visual Studio, right click the **SAPIntegration** solution, and then select **Build Solution**.

2. Once the build succeeds, right click the **SAPIntegration** solution, and then click **Deploy Solution**.

3. In the deployment window, the **Deployment Endpoint** is a read-only property and the value is derived from the **BizTalk Service URL/Namespace** set in the message flow surface. However, you must provide the ACS Namespace for BizTalk Services, Issuer Name, and Shared Secret.

4. Select **Deploy**. The Visual Studio Output pane displays the deployment progress and result. The URL where the bridge is deployed is also displayed in the Output pane. For this tutorial, the bridge is deployed at `http://*<mybiztalkservicename>*.biztalk.windows.net/default/**B2BConnector**`.

## See Also
[Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server](/Topic/Tutorial__Using_Azure_BizTalk_Services_to_Integrate_with_an_On-Premises_SAP_Server.md)

