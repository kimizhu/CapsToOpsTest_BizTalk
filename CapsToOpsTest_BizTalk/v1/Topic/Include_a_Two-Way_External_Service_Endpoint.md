---
description: na
keywords: na
pagetitle: Include a Two-Way External Service Endpoint
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88625036-f58b-4a38-9726-d2c40f24fea0
---
# Include a Two-Way External Service Endpoint
Add a two-way external service endpoint to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. Use this to route a message to a WCF external service that takes a request and sends back a response message.

> [!IMPORTANT]
> The service you wish to represent as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] must already be configured. You cannot configure a service as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

## Secure Message Transfer between the Bridge and the Service Endpoint
In scenarios involving message transfer between WCF client and services, both the client and service authentication is mandated. In routing scenarios where a bridge sends a message to a WCF service, the bridge is the client and the WCF endpoint where the message is routed to is the service. [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides support for using certificates to authenticate both the client and the service. This support is limited to services with `basicHttpBinding` and `ws2007HttpBinding`.

The security configuration and the certificate information must be included in the binding and service behavior configuration sections service’s configuration file. Also, the client’s certificate must be available in the artifact store for the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription where the bridge (that sends the message to the service endpoint) eventually gets deployed. For instructions on how to upload the certificate to the artifact store, see [Certificates](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md#BKMK_Certs).

> [!IMPORTANT]
> The certificate must be available in the artifact store before you deploy the bridge. To ensure that the bridge gets deployed successfully, after uploading the certificate, wait for 30 seconds before deploying the bridge.

At a very high-level, these are the steps that you must perform to enable certificate authentication between the bridge and the WCF service endpoint.

- As part of your service configuration, add a new binding configuration to use certificate-based security.

- Add a new service behavior configuration and include the configuration information about the client’s and server’s certificate.

## Adding a Two-way External Service Endpoint
This section provides information on how to add a two-way external service endpoint.

#### To add a two-way external service endpoint to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], as described in [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface, select **Properties**. In the **BizTalk Service URL** property, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **Two-Way External Service Endpoint** component to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface.

   > [!NOTE]
   > This adds a configuration file to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. For more information about the configuration file, see [Step 5](/Topic/Include_a_Two-Way_External_Service_Endpoint.md#BKMK_Config).

4. Right-click the component, and then select **Properties**. The following table provides information about the properties:

   |Property Name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |**Associated Project Item** <br /> <br />|This is a read-only field and provides the name of the associated .config file. If you change the name of the component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface by changing the [Entity Name](/Topic/Include_a_Two-Way_External_Service_Endpoint.md#BKMK_EntityName) property, the name of the .config also changes. <br /> <br />|
   |**Endpoint Configuration Name** <br /> <br />|Name of the client endpoint configuration in the .config file that defines the address, binding, and contract for the WCF service that you are representing on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface. Because the service configuration file can have any number of endpoints defined, the endpoint name you enter for this property is matched with the endpoint configuration name in the .config file. When a match happens, the corresponding address, binding, and contract for that endpoint are considered. **Important:** The value you enter for this property is not used for updating the **name** attribute of the **endpoint** element in the associated .config file. **Important:** You must ensure that the associated .config file has at least one endpoint defined with the name you enter here. You can either update the .config manually to create the endpoint or use the Service Configuration Editor, as explained in [Step 5(a)](/Topic/Include_a_Two-Way_External_Service_Endpoint.md#BKMK_ServiceConfigEditor). <br />|
   |**Entity Name** <br /> <br />|The name of the external service component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface. This name should be unique for a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. <br /> <br />|
   |**Runtime Address** <br /> <br />|The public runtime endpoint URL where the external service is deployed. <br /> <br />|

5. When you drop the **Two-Way External Service Endpoint** component on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design surface, it adds a configuration file with the same name as the value you provided for the **Entity Name**. This configuration file must be updated to provide information about the external service’s client endpoint such as the service binding and service contract. Perform the following steps to update the configuration file:

   1. From the Solution Explorer, right-click the .config file for the **Two-Way External Service Endpoint** component, and then select **Edit WCF Configuration** to open the **Service Configuration Editor**.

   2. Expand **Endpoints** node under the **Client** node in the Tree View pane, to see the default endpoint already created. Select the default endpoint and in the **Client Endpoint** details pane, in the **General** tab, enter the following properties:

      |Property Name <br /> <br />|Description <br /> <br />|
      |-----------------|---------------|
      |**Name** <br /> <br />|Update the endpoint configuration name, for example, **TwoWayExternalService**. **Important:** Whatever value you enter here, you must enter the same value for the [Endpoint Configuration Name](/Topic/Include_a_Two-Way_External_Service_Endpoint.md#BKMK_EndpointConfig) property. <br />|
      |**Address** <br /> <br />|The complete address where the external two-way service is hosted, for example, *https://MyServices/myTwoWayExternalService*. <br /> <br />|
      |**BehaviorConfiguration** <br /> <br />|If you want to include a custom endpoint behavior configuration, and if you already have it configured as part of the Service Configuration Editor under the **Endpoint Behaviors** node, you can select that from the drop-down list. For instructions on how to add a behavior configuration, see [To add a behavior configuration](/Topic/Include_a_Two-Way_External_Service_Endpoint.md#BKMK_BehaviorConfig). <br /> <br />|
      |**Binding** <br /> <br />|Specifies the type of binding you want to use for the endpoint. For example, for a WCF external service endpoint, you can choose **basicHttpBinding**. <br /> <br />|
      |**BindingConfiguration** <br /> <br />|Using this you can enter more details about the binding such as security requirements, etc. If you want to include a binding configuration, and if you already have it configured as part of the Service Configuration Editor under the **Bindings** node, you can select that from the drop-down list. For instructions on how to add a binding configuration, see [To add a binding configuration](/Topic/Include_a_Two-Way_External_Service_Endpoint.md#BKMK_BindingConfig). <br /> <br />|
      |**Contract** <br /> <br />|Enter the contract for the service. For a WCF two-way external service, the contract must be **System.ServiceModel.Routing.IRequestReplyRouter**. <br /> <br />|

   3. From the File menu, select **Save** and then select **Exit**.

   4. Open the configuration file and verify that the values you entered in the Service Configuration Editor are reflected in the configuration file. A sample configuration file for an external two-way service endpoint looks like the following:

      ```
      <configuration>
          <system.serviceModel>
              <bindings>
                  <basicHttpBinding>
                      <binding name="ServiceBinding">
                          <security mode="Message">
                              <transport clientCredentialType="Certificate">
                          </security>
                      </binding>
                  </basicHttpBinding>
              </bindings>
              <client>
                  <endpoint behaviorConfiguration="ServiceCredentialBehavior" address="http://MyServices/myTwoWayExternalService" binding="basicHttpBinding"
                      bindingConfiguration="ServiceBinding" contract="System.ServiceModel.Routing.IRequestReplyRouter"
                      name="TwoWayExternalService" />
              </client>
          </system.serviceModel>
      </configuration>
      ```

#### To add a behavior configuration

1. In the Service Configuration Editor, from the Tree View pane, expand **Advanced**, right-click **Endpoint Behaviors**, and then select **New Endpoint Behavior Configuration**.

2. In the **Behavior** details pane, enter a name for the behavior, for example, **ServiceCredentialBehavior**. The same name will be available in the **BehaviorConfiguration** drop-down list in Step 4(b) above.

3. In the **Behavior element extension position** area, select **Add**, from the **Available Elements** box, select the element that you want to add (e.g. **clientCredentials**), and then select **Add** again. This adds the **clientCredentials** behavior extension in the tree structure.

4. Expand the **clientCredentials** section and enter the required properties for **clientCertificate** and **serviceCertificate**.

5. In the Tree View pane, go back to the service endpoint that you created, and select the newly created endpoint behavior configuration from the **BehaviorConfiguration** drop-down list.

#### To add a binding configuration

1. In the Service Configuration Editor, from the Tree View pane, right-click **Bindings**, and then select **New Binding Configuration**.

2. In **Create a New Binding**, select the same binding that you specified in Step 4(b) above, and then select **OK**.

3. In the binding details pane, on the **Binding** tab, for the **Name** property, enter a name for the binding configuration, for example, **ServiceBinding**. The same name is available in the **BindingConfiguration** drop-down list in Step 4(b) above.

4. In the binding details pane, on the **Security** tab, for the **Mode** drop-down list, select **Message** and for the **MessageClientCredentialType** option, select **Certificate**.

5. In the Tree View pane, go back to the service endpoint that you created, and select the newly created binding configuration from the **BindingConfiguration** drop-down list.

6. If you save and exit the configuration editor now, and open the configuration file in an XML editor, you notice that the following has been added to the service configuration file. This excerpt assumes that the binding you selected was **basicHttpBinding**.

   ```
   <bindings>
     <basicHttpBinding>
       <binding name="ServiceBinding">
         <security mode="Message">
           <transport clientCredentialType="Certificate" />
         </security>
       </binding>
     </basicHttpBinding>
   </bindings>
   ```

## See Also
[Add a Message Destination to the bridge](/Topic/Add_a_Message_Destination_to_the_bridge.md)

