---
description: na
keywords: na
pagetitle: Include a One-Way Relay Endpoint
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2479b68c-3d74-462c-99ed-9d9775e57575
---
# Include a One-Way Relay Endpoint
Add a one-way relay endpoint to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. Use this destination to route a message to relay endpoint that takes a request but does not return a response.

> [!IMPORTANT]
> The relay endpoint you wish to represent as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] must already be configured. You cannot configure a relay endpoint as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

### To add a one-way relay endpoint to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] project, as described in [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, select **Properties**. For the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **One-Way Relay Endpoint** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area.

   > [!NOTE]
   > This adds a configuration file to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. For more information about the configuration file, see [Step 5](/Topic/Include_a_One-Way_Relay_Endpoint.md#BKMK_Config).

4. Right-click the component, and then select **Properties**. The following table provides information about the properties:

   |Property Name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |**Associated Project Item** <br /> <br />|This is a read-only field and provides the name of the associated .config file. If you change the name of the component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area by changing the [Entity Name](/Topic/Include_a_One-Way_Relay_Endpoint.md#BKMK_EntityName) property, the name of the .config also changes. <br /> <br />|
   |**Endpoint Configuration Name** <br /> <br />|Name of the client endpoint configuration in the .config file that defines the address, binding, and contract for the WCF relay service that you are representing on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface. Because the service configuration file can have any number of endpoints defined, the endpoint name you enter for this property is matched with the endpoint configuration name in the .config file. When a match happens, the corresponding address, binding, and contract for that endpoint are considered. **Important:** The value you enter for this property is not used for updating the **name** attribute of the **endpoint** element in the associated .config file. **Important:** You must ensure that the associated .config file has at least one endpoint defined with the name you specify here. You can either update the .config manually to create the endpoint or use the Service Configuration Editor, as explained in [Step 5(a)](/Topic/Include_a_One-Way_Relay_Endpoint.md#BKMK_ServiceConfigEditor). <br />|
   |**Entity Name** <br /> <br />|The name of the relay endpoint component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area. This name should be unique for a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. <br /> <br />|
   |**Runtime Address** <br /> <br />|The public runtime endpoint URL where the relay service is deployed. <br /> <br />|

5. When you drop the **One-Way Relay Endpoint** component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area, it adds a configuration file with the same name as the value you entered for the **Entity Name**. This configuration file must be updated to provide information about the client endpoint for the relay such as the service binding and service contract. Perform the following steps to update the configuration file.

   1. From the Solution Explorer, right-click the .config file for the **One-Way Relay Endpoint** component, and then select **Edit WCF Configuration** to open the **Service Configuration Editor**.

   2. Expand **Endpoints** node under the **Client** node in the Tree View pane, to see the default endpoint already created. Select the default endpoint and in the **Client Endpoint** details pane, in the **General** tab, enter the following properties.

      |Property Name <br /> <br />|Description <br /> <br />|
      |-----------------|---------------|
      |**Name** <br /> <br />|Update the endpoint configuration name, for example, **OneWayRelay**. **Important:** Whatever value you enter here is reflected for the [Endpoint Configuration Name](/Topic/Include_a_One-Way_Relay_Endpoint.md#BKMK_EndpointConfig) property. <br />|
      |**Address** <br /> <br />|The address where the relay endpoint is hosted on the [!INCLUDE[sb2](/Token/sb2_md.md)]. You must update the address to include your [!INCLUDE[sb2](/Token/sb2_md.md)] namespace and the complete URL for the relay service. <br /> <br />|
      |**BehaviorConfiguration** <br /> <br />|If you want to include a custom endpoint behavior configuration, and if you already have it configured as part of the Service Configuration Editor under the **Endpoint Behaviors** node, you can select that from the drop-down list. For instructions on how to add a behavior configuration, see [To add a behavior configuration](/Topic/Include_a_One-Way_Relay_Endpoint.md#BKMK_BehaviorConfig). <br /> <br />|
      |**Binding** <br /> <br />|Specifies the type of binding you want to use for the endpoint. For example, for a relay endpoint, you can choose **basicHttpRelayBinding**. <br /> <br />|
      |**BindingConfiguration** <br /> <br />|Using this you can specify more details about the binding such as security requirements, etc. If you want to include a binding configuration, and if you already have it configured as part of the Service Configuration Editor under the **Bindings** node, you can select that from the drop-down list. For instructions on how to add a binding configuration, see [To add a binding configuration](/Topic/Include_a_One-Way_Relay_Endpoint.md#BKMK_BindingConfig). <br /> <br />|
      |**Contract** <br /> <br />|Enter the contract for the service. For a one-way relay endpoint, the contract must be **System.ServiceModel.Routing.ISimplexDatagramRouter**. <br /> <br />|

   3. From the File menu, select **Save**, and then select **Exit**.

   4. Open the configuration file and verify that the values you entered in the Service Configuration Editor are reflected in the configuration file. A sample configuration file for a one-way relay endpoint looks like the following:

      ```
      <configuration>
          <system.serviceModel>
              <behaviors>
                  <endpointBehaviors>
                      <behavior name="ServiceCredentialBehavior">
                          <transportClientEndpointBehavior>
                              <tokenProvider>
                                  <sharedSecret issuerName="owner" issuerSecret="****************" />
                              </tokenProvider>
                          </transportClientEndpointBehavior>
                      </behavior>
                  </endpointBehaviors>
              </behaviors>
              <bindings>
                  <basicHttpRelayBinding>
                      <binding name="ServiceBinding">
                        <security mode ="Transport" relayClientAuthenticationType ="RelayAccessToken" />
                      </binding>
                  </basicHttpRelayBinding>
              </bindings>
              <client>
                  <endpoint behaviorConfiguration="ServiceCredentialBehavior" address="/OneWayRelayEndpoint" binding="basicHttpRelayBinding"
                      bindingConfiguration="ServiceBinding" contract="System.ServiceModel.Routing.ISimplexDatagramRouter"
                      name="OneWayRelay" />
              </client>
          </system.serviceModel>
      </configuration>
      ```

### To add a behavior configuration

1. In the Service Configuration Editor, from the Tree View pane, expand **Advanced**, right-click **Endpoint Behaviors**, and then select **New Endpoint Behavior Configuration**.

2. In the **Behavior** details pane, enter a name for the behavior, for example, **ServiceCredentialBehavior**. The same name is available in the **BehaviorConfiguration** drop-down list in Step 4 (b) above.

3. In the **Behavior element extension position** area, select **Add**, from the **Available Elements** box, select **transportClientEndpointBehavior**, and then select **Add** again. You must add this element to specify the [!INCLUDE[sb2](/Token/sb2_md.md)] credentials for a particular endpoint.

4. In the Tree View pane, go back to the service endpoint that you created, and select the newly created endpoint behavior configuration from the **BehaviorConfiguration** drop-down list.

5. If you save and exit the configuration editor now, and open the configuration file in an XML editor, you notice that the following has been added to the service configuration file:

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

6. For a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, you only need to include the token credentials. So, you must remove the **clientCredentials** element and add the value for Issuer Name and Issuer Secret for the **tokenProvider** credentials. The section of the configuration file now resembles the following:

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

### To add a binding configuration

1. In the Service Configuration Editor, from the Tree View pane, right-click **Bindings**, and then select **New Binding Configuration**.

2. In the **Create a New Binding** box, select the same binding that you specified in Step 4(b) above, and then select **OK**.

3. In the binding details pane, on the **Binding** tab, for the **Name** property, enter a name for the binding configuration, for example, **ServiceBinding**. The same name will be available in the **BindingConfiguration** drop-down list in Step 4 (b) above.

4. In the Tree View pane, go back to the service endpoint that you created, and select the newly created binding configuration from the **BindingConfiguration** drop-down list.

5. If you save and exit the configuration editor now, and open the configuration file in an XML editor, you notice that the following has been added to the service configuration file. This excerpt assumes that the binding you selected was **basicHttpRelayBinding**.

   ```
   <bindings>
     <basicHttpRelayBinding>
       <binding name="ServiceBinding" />
     </basicHttpRelayBinding>
   </bindings>
   ```

6. For a [!INCLUDE[sb2](/Token/sb2_md.md)] relay endpoint, you must add the **security** element and set the **mode** and **relayClientAuthenticationType** attributes for the element. The section of the configuration file would now resemble the following:

   ```
   <bindings>
     <basicHttpRelayBinding>
       <binding name="ServiceBinding">
         <security mode ="Transport" relayClientAuthenticationType ="RelayAccessToken" />
       </binding>
     </basicHttpRelayBinding>
   </bindings>
   ```
   Setting **relayClientAuthenticationType** to **RelayAccessToken** specifies that the clients of the service are required to present a security token issued by Access Control to the [!INCLUDE[sb2](/Token/sb2_md.md)] when sending messages.

## See Also
[Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md)

