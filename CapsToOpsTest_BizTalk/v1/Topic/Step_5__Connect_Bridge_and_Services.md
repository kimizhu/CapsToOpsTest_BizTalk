---
description: na
keywords: na
pagetitle: Step 5: Connect Bridge and Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5780b286-e997-4b09-8217-9ebe1103a5b4
---
# Step 5: Connect Bridge and Services
The previous topics in the tutorial demonstrated how to create the two relay services and how to configure the [!INCLUDE[request_response](/Token/request_response_md.md)]. This topic demonstrates how to connect the [!INCLUDE[bridge](/Token/bridge_md.md)] to the two services so that the message that comes to the [!INCLUDE[bridge](/Token/bridge_md.md)] is routed to the right relay service. And then finally, according to the [Business Scenario](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md#BKMK_Scenario), this tutorial demonstrates how to stamp the messages routed to the relay services with the **QuoteType** message header. To achieve these goals, perform the following three tasks:

- Add the two-way relay endpoint components to the itinerary designer to represent the two-way relay services that receive the message from the [!INCLUDE[bridge](/Token/bridge_md.md)].

- Connect the [!INCLUDE[bridge](/Token/bridge_md.md)] to the two-way relay endpoints on the [!INCLUDE[bridge](/Token/bridge_md.md)] and set the routing condition.

- Stamp the messages sent to the relay services with the **QuoteType** message header.

## Represent Relay Services in the BizTalk Service Project
As mentioned earlier, the tutorial already has two relay receiver services defined and one [!INCLUDE[request_response](/Token/request_response_md.md)] configured to process the messages. While the [!INCLUDE[bridge](/Token/bridge_md.md)] is part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], the relay receiver services are two separate projects in themselves. The [!INCLUDE[bridge](/Token/bridge_md.md)] and the relay receiver services must be connected together so that the messages processed by the [!INCLUDE[bridge](/Token/bridge_md.md)] can be routed to the services, and vice versa, the response from the relay services can be routed back to the [!INCLUDE[bridge](/Token/bridge_md.md)] and then to the client. To enable this scenario, the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface provides a **Two-Way Relay Endpoint** component that you can include in the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] to represent two-way relay services, **RelayReceiverServiceA** and **RelayReceiverServiceB**.

#### To represent RelayReceiverServiceA in the project

1. From the **Toolbox**, drag and drop the **Two-Way Relay Endpoint** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface.

2. When you drop the component on the itinerary designer, it adds a configuration file to the project. This configuration file must be updated to provide information about the endpoint for the relay service. Perform the following steps to update the configuration file.

   1. From the Solution Explorer, right-click the .config file for the **Two-Way Relay Endpoint** component and then select **Edit WCF Configuration** to open the **Service Configuration Editor**.

   2. Expand the **Endpoints** node under the **Client** node in the tree view pane, and then select the existing endpoint **TwoWayRelayServiceReference1**. In the **Client Endpoint** details pane, in the **General** tab, enter the following properties.

      |Property Name <br /> <br />|Description <br /> <br />|
      |-----------------|---------------|
      |**Name** <br /> <br />|Enter the endpoint name, for example, **RelayService_SmallAmounts**, to represent the relay receiver service that will process messages with quotation amount less than $10000. **Important:** Whatever value you enter here, enter the same value for the **Endpoint Configuration Name** property. <br />|
      |**Address** <br /> <br />|The complete address where the relay endpoint is hosted on the [!INCLUDE[sb2](/Token/sb2_md.md)]. For this tutorial, set the address to the URL where the **RelayReceiverServiceA** is hosted. You can get the address from the command prompt that represents the RelayReceiverServiceA. Typically, the address should be &#96;https://&lt;your_servicebus_namespace&gt;.servicebus.windows.net/RelayReceiverServiceA&#96;. <br /> <br />|

   3. In the Service Configuration Editor, from the Tree View pane, expand **Advanced**, right-click **Endpoint Behaviors**, and then select **New Endpoint Behavior Configuration**.

   4. In the **Behavior** details pane, enter a name for the behavior, for example, **ServiceCredentialBehavior**.

   5. In the **Behavior element extension position** area, select **Add**, from the **Available Elements** box, select **transportClientEndpointBehavior**, and then select **Add** again. You must add this element to enter the [!INCLUDE[sb2](/Token/sb2_md.md)] credentials for a particular endpoint.

   6. In the Tree View pane, go back to the service endpoint (**RelayService_SmallAmounts**) that you created, and select the newly created endpoint behavior configuration from the **BehaviorConfiguration** drop-down list. Accept the default values for all the other properties and from the **File** menu, select **Save**. Close the dialog box.

   7. Open the config file (available under the **MessageFlowItinerary.bcs** in the Solution Explorer) in an XML editor. You will notice that the following has been added to the service configuration file:

      ```
      <behaviors>
        <endpointBehaviors>
          <behavior name="ServiceCredentialBehavior">
            <transportClientEndpointBehavior>
              <clientCredentials>
                <sharedSecret issuerName="" issuerSecret="" />
              </clientCredentials>
              <tokenProvider>
                <sharedSecret issuerName="" issuerSecret="" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
      </behaviors>
      ```
      For a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, you only need to include the token credentials. So, you must remove the **clientCredentials** element and add the value for the [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name and Issuer Secret for the **tokenProvider** credentials. The section of the configuration file would now resemble the following:

      ```
      <behaviors>
        <endpointBehaviors>
          <behavior name="ServiceCredentialBehavior">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedSecret issuerName="owner" issuerSecret="**********************" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
      </behaviors>
      ```
      Save changes and close the configuration file.

   8. On the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface, right-click the component, and then select **Properties**. The following table provides information about the properties:

      |Property Name <br /> <br />|Description <br /> <br />|
      |-----------------|---------------|
      |**Associated Project Item** <br /> <br />|A read-only field that provides the name of the associated .config file. If you change the name of the component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface by changing the **Entity Name** property, the name of the .config also changes. <br /> <br />|
      |**Endpoint Configuration Name** <br /> <br />|Name of the client endpoint configuration in the .config file that defines the address, the binding, and the contract for the WCF relay service that you are representing on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface. For this tutorial, set this property to **RelayService_SmallAmounts**. You specified the same value for the **Name** property in the previous step. <br /> <br />Because the service configuration file can have any number of endpoints defined, the endpoint name you enter for this property is matched with the endpoint configuration name in the .config file. When a match happens, the corresponding address, binding, and contract for that endpoint are considered. <br /> <br />|
      |**Entity Name** <br /> <br />|The name of the relay endpoint component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface. This name must be unique for an [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. For this tutorial, name it **SmallAmounts_Service**. <br /> <br />|
      |**Runtime Address** <br /> <br />|The public runtime endpoint URL where the relay service is deployed. <br /> <br />|

3. Save changes to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

#### To represent RelayReceiverServiceB in the project

1. From the **Toolbox**, drag and drop the **Two-Way Relay Endpoint** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface.

2. When you drop the component on the design surface, it adds a configuration file to the project. This configuration file must be updated to provide information about the endpoint for the relay service. Perform the following steps to update the configuration file.

   1. From the Solution Explorer, right-click the .config file for the **Two-Way Relay Endpoint** component and then select **Edit WCF Configuration** to open the **Service Configuration Editor**.

   2. Expand the **Endpoints** node under the **Client** node in the tree view pane, and then select the existing endpoint **TwoWayRelayServiceReference1**. In the **Client Endpoint** details pane, in the **General** tab, enter the following properties.

   3. In the Service Configuration Editor, from the Tree View pane, expand **Advanced**, right-click **Endpoint Behaviors**, and then select **New Endpoint Behavior Configuration**.

   4. In the **Behavior** details pane, enter a name for the behavior, for example, **ServiceCredentialBehaviorB**.

   5. In the **Behavior element extension position** area, select **Add**, from the **Available Elements** box, select **transportClientEndpointBehavior**, and then select **Add** again. You must add this element to enter the [!INCLUDE[sb2](/Token/sb2_md.md)] credentials for a particular endpoint.

   6. In the Tree View pane, go back to the service endpoint (**RelayService_LargeAmounts**) that you created, and select the newly created endpoint behavior configuration from the **BehaviorConfiguration** drop-down list. Accept the default values for all the other properties and from the **File** menu, select **Save**. Close the dialog box.

   7. Open the config file (available under the **MessageFlowItinerary.bcs** node in the Solution Explorer) in an XML editor. You will notice that the following has been added to the service configuration file:

      ```
      <behaviors>
        <endpointBehaviors>
          <behavior name="ServiceCredentialBehaviorB">
            <transportClientEndpointBehavior>
              <clientCredentials>
                <sharedSecret issuerName="" issuerSecret="" />
              </clientCredentials>
              <tokenProvider>
                <sharedSecret issuerName="" issuerSecret="" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
      </behaviors>
      ```
      For a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, you only need to include the token credentials. So, you must remove the **clientCredentials** element and add the value for the [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name and Issuer Secret for the **tokenProvider** credentials. The section of the configuration file would now resemble the following:

      ```
      <behaviors>
        <endpointBehaviors>
          <behavior name="ServiceCredentialBehaviorB">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedSecret issuerName="owner" issuerSecret="**********************" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
      </behaviors>
      ```
      Save changes and close the configuration file.

   8. On the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface, right-click the component, and then select **Properties**. The following table provides information about the properties:

3. Save changes to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

## Connect the [!INCLUDE[bridge](/Token/bridge_md.md)] with Relay Services
This section provides instructions on how to connect the [!INCLUDE[bridge](/Token/bridge_md.md)] with the two relay services. As part of the Connectors, enter the ‘route conditions’ that govern when a message is routed to **RelayReceiverServiceA** and when it’s routed to **RelayReceiverServiceB**. The following procedure provides instructions on how to connect the [!INCLUDE[bridge](/Token/bridge_md.md)] with the two services and how to set the routing conditions.

#### To connect [!INCLUDE[bridge](/Token/bridge_md.md)] with relay services

1. In the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], select the **Connector** component under the **[!INCLUDE[bridge](/Token/bridge_md.md)]s** category in the **Toolbox**.

2. Take the mouse pointer to the right-end of the [!INCLUDE[bridge](/Token/bridge_md.md)] (denoted by a red dot when you move the cursor over the component). The mouse pointer changes to show a small “**S**” sign denoting that this component is the source for the Connector. Select and hold the mouse at the dot, drag it to the left end of the target component, **SmallAmounts_Service** relay endpoint. The cursor changes again to show a small “**T**” denoting the target; release the mouse. The two components are now connected.

   Repeat this step to connect the [!INCLUDE[bridge](/Token/bridge_md.md)] to the other relay service endpoint, **LargeAmounts_Service**.

3. Set the routing conditions on the two Connectors. The routing condition must be set on the quote amount in the request message that the [!INCLUDE[bridge](/Token/bridge_md.md)] receives. The procedure, [To extract and promote properties in the pre-transform Enrich stage](/Topic/Step_4_a):%20Configure%20the%20Request%20Bridge.md#BKMK_ReqP_Enrich), already configures the [!INCLUDE[bridge](/Token/bridge_md.md)] to extract the value of the quote amount into a property called **QuoteAmount**. Here, you use that property to define the routing condition.

   1. Right-click the route Connector between [!INCLUDE[request_response](/Token/request_response_md.md)] and **SmallAmounts_Service** relay endpoint, and then select **Properties**. In the **Properties** pane, for the **Filter Condition** property, select the ellipsis **(…)** button to the open the **Route Filter Configuration** dialog box.

   2. In the dialog box, select the **Filter** option, and then enter the following filter string:

      ```
      QuoteAmount < 10000
      ```
      > [!NOTE]
      > Use standard SQL 92 syntax for filter expressions.

      Select **OK** to save the changes and exit.

   3. Repeat the previous step for the Connector between [!INCLUDE[request_response](/Token/request_response_md.md)] and **LargeAmounts_Service** relay endpoint and enter the filter string as:

      ```
      QuoteAmount >= 10000
      ```
      The [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface resembles the following:

      ![](/Image/BridgesSvc_AllConnected.gif)

4. Save changes to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

With these changes to the project, messages that are sent to the [!INCLUDE[bridge](/Token/bridge_md.md)] are appropriately routed to the right relay service based on the quote amount.

## <a name="BKMK_RouteAction"></a>Include Custom Headers in the Message
The other requirement of the [Business Scenario](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md#BKMK_Scenario) as part of the routing configurations is to ensure that the messages sent to the relay services are stamped with a header called **QuoteType**. The value of the **QuoteType** header must be set to **SmallAmounts** (if the message is routed to the relay endpoint **SmallAmounts_Service**) or **LargeAmounts** (if the message is routed to the relay endpoint **LargeAmounts_Service**).

#### To add custom headers to the message

1. Right-click the route Connector between the [!INCLUDE[bridge](/Token/bridge_md.md)] and the **SmallAmounts_Service** relay endpoint, and then select **Properties**. In the Properties pane, for the **Route Action** property, select the ellipsis **(…)** button to the open the **Route Actions** dialog box.

2. In the **Route Actions** dialog box, select **Add** to open the **Add Route Action** dialog box. In the **Add Route Action** dialog box, do the following:

   The dialog box resembles the following:

   ![](/Image/BridgesSvc_RouteAction.gif)

   Select **OK** in the **Add Route Action** dialog box and then select **OK** again in the **Route Connections** dialog box.

3. Repeat the last step on the route Connector between the [!INCLUDE[bridge](/Token/bridge_md.md)] and the **LargeAmounts_Service** relay endpoint. However, for that Connector you must enter the value in the **Expression** field as **'LargeAmounts'**

4. Save changes to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

## See Also
[Tutorial: Using BizTalk Service Bridges to Send and Receive Messages from Service Bus Relay Service](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md)

