---
description: na
keywords: na
pagetitle: Create an XML Request-Reply Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e5fedb4-9ab1-4470-aa8a-204633391da7
---
# Create an XML Request-Reply Bridge
This section lists the steps create an [!INCLUDE[request_response](/Token/request_response_md.md)] in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]s have different stages. In this topic:

1. [Add the Bridge to the BizTalk Services project](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_AddTwoWay)

2. [Enter the request schemas](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_AddSchemas)

3. [Configure the Validate stage](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Validate)

4. [Configure the Enrich Stage and its Properties](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Enrich)

5. [Configure the Transform stage](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Transform)

6. [Configure the Enrich Stage (post- Transform)](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_EnrichPostTrans)

7. [Configure the Enrich Stage for the Response Message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_EnrichResp)

8. [Configure the Transform Stage for the Response Message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_TransformResp)

9. [Configure the Enrich Stage (post-Transform) for the Response Message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_EnrichPostResp)

10. [Configure the Reply Action Before Routing the Response Message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Reply)

## <a name="BKMK_AddTwoWay"></a>Add the Bridge to the BizTalk Services project

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md) lists the steps.

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area and select **Properties**. In **BizTalk Service URL**, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **[!INCLUDE[request_response](/Token/request_response_md.md)]** to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area. A *.BridgeConfig* file is added to the solution.

4. Right-click the [!INCLUDE[bridge](/Token/bridge_md.md)], select **Properties**, and then enter the following properties:

   |Property Name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |**Associated Project Item** <br /> <br />|Read-only: The name of the associated .BridgeConfig file. To change the name of the file, change the **Entity Name** property. <br /> <br />|
   |**Entity Name** <br /> <br />|The name of the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area. This name should be unique for the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. The name of the *.BridgeConfig* file is the same as the value you enter here. <br /> <br />|
   |**Relative Address** <br /> <br />|The relative address where the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] is hosted on [!INCLUDE[azure_1](/Token/azure_1_md.md)]. This address combined with the [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL you enter in Step 2 creates the complete URL for the [!INCLUDE[bridge](/Token/bridge_md.md)]. <br /> <br />For example, if the [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL is **MyBizTalkService** and the relative address of the [!INCLUDE[bridge](/Token/bridge_md.md)] is **UpdateCustomers**, the URL for the endpoint on the [!INCLUDE[sb2](/Token/sb2_md.md)] is *https://MyBizTalkService.biztalk.windows.net/default/UpdateCustomers*. <br /> <br />|
   |**Route Ordering Table** <br /> <br />|Enter the routing order of the message from the [!INCLUDE[bridge](/Token/bridge_md.md)] to other components of the message flow. See [The Routing Order](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_Order). <br /> <br />|
   |**Runtime Address** <br /> <br />|The public runtime endpoint URL where the bridge is deployed. <br /> <br />|
   |**Track Properties** <br /> <br />|Set this property to define which message properties are tracked by the [!INCLUDE[bridge](/Token/bridge_md.md)]. See [Tracking Messages Processed by the Bridge](/Topic/Tracking_Messages_Processed_by_the_Bridge.md). <br /> <br />|

5. Click **Save**.

## <a name="BKMK_TwoWay_AddSchemas"></a>Enter the request schemas
A single [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] can have multiple bridges and multiple schemas. For ease of use and to save on processing time, you can associate schemas with bridges. In other words, you can require that a specific bridge can only process messages that conform to a specific schema or a set of schemas. This section lists the steps to create this association.

1. Add the schemas to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md) lists the steps. Repeat this step to add any number of schemas that you need for your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

2. Double-click the [!INCLUDE[request_response](/Token/request_response_md.md)] to open the itinerary designer.

   > [!NOTE]
   > The itinerary designer is a read-only area. You cannot add or remove a stage or an activity from the itinerary designer.

3. On the [!INCLUDE[bridge](/Token/bridge_md.md)] design area in the **Message Types** box, select the add icon [ ![](/Image/IntSvcs_Bridges_Add_Icon.gif) ] to open **Message Type Picker**. In **Message Type Picker**:

   1. From the **Available message types** box, select the schema for the Request message.

   2. Select the right arrow icon [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ] to associate the Request schema with the [!INCLUDE[bridge](/Token/bridge_md.md)].

   3. Select the right arrow icon [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ] under **Response Message Type** to associate the Response schema with the [!INCLUDE[bridge](/Token/bridge_md.md)].

   4. Select **OK**. The schema that you selected is now listed under the **Message Type** box.

      **Additional**:

      - You cannot add multiple schemas at the same time. To associate more schemas with the [!INCLUDE[bridge](/Token/bridge_md.md)], repeat this step.

      - To remove a schema association with the [!INCLUDE[bridge](/Token/bridge_md.md)], select the schema from the **Message Type** box, and then press the delete icon [ ![](/Image/IntSvcs_Bridges_Delete_Icon.gif) ].

      - To replace one schema association with another, click the edit button [ ![](/Image/IntSvcs_Bridges_Edit_Icon.gif) ] to reopen **Message Type Picker**.

4. Click **Save**.

## <a name="BKMK_TwoWay_Validate"></a>Configure the Validate stage for the Request message
In the **Validate** stage, you can enter whether the stage does any schema validation on the incoming request message and whether the validation warnings can be propagated back to the client as exceptions.

1. Double-click the [!INCLUDE[bridge](/Token/bridge_md.md)] to open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design area.

2. Select the **Validate** stage. In **Properties**, set **IsEnabled** to **True** or **False**. When **True**, the stage validates the incoming request message against the schemas you previously added. If **False**, there is no schema validation and the message is simply passed through to the next stage.

   **Additional**:

   - To include any custom code that executes *before* the message enters the **Validate** stage, set the **On Enter Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

   - To include any custom code that executes *after* the message exits the **Validate** stage, set the **On Exit Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

3. Select the **Xml Validate** activity. In **Properties**, set **Report Warnings As Errors** property to **True** or **False**. When **True**, the [!INCLUDE[bridge](/Token/bridge_md.md)] reports any warnings as errors encountered during XML validation against a schema and returns them back to the client that sent the request message. A validation warning is thrown as an exception and the validation fails. See [Validation and the Schema Object Model](http://msdn.microsoft.com/library/aa310912%28v=VS.71%29.aspx) to understand the warnings and errors in XML schema validation.

4. Click **Save**.

## <a name="BKMK_TwoWay_Enrich"></a>Configure the Enrich Stage (and its Properties) for the Request message
The **Enrich** stage enables message enrichment by defining properties, the values for which can be derived from the message header (standard or custom), through default properties promoted by [!INCLUDE[af_integration](/Token/af_integration_md.md)], from an external data source (only [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] tables are supported), or from an element within the message body. These properties can then be used to either route the message to a destination endpoint or for further processing by the message receiving entity. This section lists the steps for performing each of the following actions:

- Assign message header values to properties.

- Use default properties or system properties promoted by [!INCLUDE[af_integration](/Token/af_integration_md.md)].

- Look up an external data source

- Extract values from a message body element using Xpath

**Important**:

- The property names you enter in this stage are not case-sensitive.

- The property you enter in this stage is not for Route or Reply Actions *unless* you save the [!INCLUDE[msgflow](/Token/msgflow_md.md)]. See [Route and Reply Actions: Bridging Protocol Mismatch](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md) for more details on Route and Reply.

You can choose whether you want to perform any of these actions by turning the **Enrich** stage on or off.

**Steps**:

1. Double-click the [!INCLUDE[request_response](/Token/request_response_md.md)] to open the itinerary designer.

2. Select the **Enrich** stage. In **Properties**, set the **IsEnabled** property to **True** or **False**.

   > [!NOTE]
   > When **True** and there is no property defined, then the [!INCLUDE[bridge](/Token/bridge_md.md)] does not throw an error when configuring the [!INCLUDE[bridge](/Token/bridge_md.md)] (design-time) nor when processing the message (run-time).

   **Additional**:

   - To include any custom code that executes *before* the message enters this stage, set the **On Enter Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

   - To include any custom code that executes *after* the message exits this stage, set the **On Exit Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

3. Within the **Enrich** stage, select the **Enrich** activity. In **Properties**, select the ellipsis button **(…)** against the **Property Definition** property to open **Property Definitions**.

4. In **Property Definitions**, select **Add**. In **Add Property**, you can use values from various sources and include them in the message as properties. These properties and their values can then be used later for other processing tasks, like routing messages to different destinations based on property values (see [The Routing Action](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_RoutingAction)). The following table lists the different sources and ways to add properties to the message:

   |Source <br /> <br />|How To <br /> <br />|
   |----------|----------|
   |Assign message header values to properties <br /> <br />||
   |Use system-promoted properties <br /> <br />||
   |Look up an external data source <br /> <br />||
   |Extract values from within the message using XPath <br /> <br />||

#### To assign message header values to properties

1. In **Add Property**, do the following:

   > [!NOTE]
   > This table lists only the fields required for the header to property assignment operation, which is relevant only for messages that are transferred using the message transfer protocols such as SOAP, HTTP, FTP, and SFTP. So, the following steps are relevant only if you select **HTTP**, **SOAP**, **FTP**, or **SFTP** from the **Type** drop-down list. Also, depending on what you select for the **Type** drop-down list, the required fields are outlined in red and the other fields are greyed out.

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Source (Read From) <br /> <br />|Type <br /> <br />|Specifies the message type from which the header values ae extracted. For assigning header values to properties, the possible values are **SOAP**, **HTTP**, **FTP**, **SFTP**, and **Brokered**. <br /> <br />|
   |Source (Read From) <br /> <br />|SOAP Header Namespace (only if the **Type** is set to **SOAP**) <br /> <br />|Specifies the namespace of the custom SOAP header. For example, in the following excerpt, the namespace for the **MessageType** custom header is highlighted: <br /> <br />DELETED CODE **Important:** This field is greyed out if you select a standard header from the **Identifier** drop-down list. You must enter a namespace only for custom SOAP headers; however it’s not a mandatory property.This field is also greyed out if the Type is set to **HTTP**, **FTP**, **SFTP**, or **Brokered**. <br />|
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|Specifies the name of message header property, the value of which you want to extract and assign to a property that you are defining in this dialog box. If we take the same excerpt as above, the identifier would be **MessageType**. <br /> <br />You can also specify custom headers here. For FTP and SFTP, the drop-down lists the standard identifiers. For HTTP message type, because there’s a huge list of standard headers, the drop-down does not list any headers; you can enter the name of the header in such a case. Also, for SOAP, HTTP, and Brokered message types, you can also list a custom header whose value you want to assign to another property. <br /> <br />To understand this better, look at this example. Let’s assume a SOAP message header looks like the following: <br /> <br />DELETED CODE <br /> <br />In this excerpt, **PONumber** is a custom SOAP header whose value is PO1234. So, if you set the Identifier to **PONumber**, the value **PO1234** is assigned to the property that you are defining here. <br /> <br />|
   |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specifies the name of the property that you are defining. The value of this property is set to the value that is extracted from the message header property you specified earlier. <br /> <br />To continue using the same example as above, if you set the Property Name to **P1** and **Identifier** to **PONumber**, the value of **P1** is set to **PO1234**. <br /> <br />|
   |Property (Write To) <br /> <br />|Data Type <br /> <br />|Specifies the data type for the property. You can select a value from the drop-down list. <br /> <br />|

2. Click **OK** in the **Add Property** dialog box. The dialog boxes should now resemble the following:

   ![](/Image/IntSvcs_Enrich_HeaderPropertyAssgn.gif)

   So what does this screen capture depict? It means that if the incoming message is a SOAP message with a SOAP header name as **PONumber** and header namespace as `http://schemas.microsoft.com/integration/promotedpropertiesinfo`, then a **P1** with data type **string** is created and the value of header is assigned to this property.

3. To update or remove a property definition, you can select the property definition in the dialog box and then click **Edit** or **Remove**. Click **OK** in the **Property Definition** dialog box and then click **Save** to save changes to the [!INCLUDE[msgflow](/Token/msgflow_md.md)].

#### To use system-promoted properties

1. In **Add Property**, do the following:

   > [!NOTE]
   > This table lists only the fields required for the system-promoted properties assignment to the message. Also, depending on what you select for the **Type** drop-down list, the required fields are outlined in red and the other fields are greyed out.

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Source (Read From) <br /> <br />|Type <br /> <br />|For using system-promoted properties, select **System** from the drop-down list. <br /> <br />|
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|Specifies the name of system-promoted property, the value of which you want to extract and assign to a property that you are defining in this dialog box. <br /> <br />|
   |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specifies the name of the property that you are defining. The value of this property is set to the value that is extracted from the system-promoted property you specified earlier. <br /> <br />|
   |Property (Write To) <br /> <br />|Data Type <br /> <br />|Specifies the data type for the property. You can select a value from the drop-down list. <br /> <br />|

#### To lookup an external data source

1. In **Add Property**, do the following:

   > [!NOTE]
   > This table lists only the fields required for the lookup operation. So, the following steps are relevant only if you select **Lookup** from the **Type** drop-down list. Also, depending on what you select for the **Type** drop-down list, the required fields are outlined in red and the other fields are greyed out.

   > [!IMPORTANT]
   > For this release, you can only lookup from a [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table.

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Source (Read From) <br /> <br />|Type <br /> <br />|For a lookup operation, select **Lookup** from the drop-down list. <br /> <br />|
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|From the drop-down list, select an already configured provider <br /> <br />If you haven’t already configured a provider, then configure one: <br /> <br /><ol><li>From the **Identifier** drop-down list, select **Configure New**. </li><li>In the **Provider Configuration** dialog box, specify the following values: <br /> <br />   **Provider Name:** <br /> <br />   Specify a name for the provider <br /> <br />   **Connection String:** <br /> <br />   Specify a valid connection string to connect to a [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table <br /> <br />   **Table Name:** <br /> <br />   Specify the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table name from which you want to do a data lookup <br /> <br />   **Query In Column:** <br /> <br />   Specify a column name in the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table, the values of which are used as the input query for performing the data lookup <br /> <br />   **Query Out Column:** <br /> <br />   Specify a column name in the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table, the value is the output value that is eventually assigned to the looked up property. </li><li>Click **OK** to add the provider configuration. </li> </ol>|
   |Source (Read From) <br /> <br />|Lookup Property <br /> <br />|From the drop-down list, select a property that you must have already defined. The value of this property is passed on to the **Query In Column** specified in the provider configuration above. <br /> <br />|
   |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specify a name for the property that contains the looked up value. The value of this property is derived from the value of the **Query Out Column** in the provider configuration above. <br /> <br />|
   |Property (Write To) <br /> <br />|Data Type <br /> <br />|Specifies the data type for the property. You can select a value from the drop-down list. <br /> <br />|

2. Click **OK** in the **Add Property** dialog box.  The dialog boxes should resemble the following:

   ![](/Image/IntSvcs_Enrich_Lookup.gif)

   So what do these dialog boxes depict? This is how the logic flows (explained using the same purchase order example as above):

   - The [!INCLUDE[bridge](/Token/bridge_md.md)] looks up the value of P1 (**PO1234**) in the input query column (**P_Order**) in the table (**TempTable**) defined in the **MyProvider** provider configuration.

   - The [!INCLUDE[bridge](/Token/bridge_md.md)] then picks up the value corresponding to **PO1234** from the output query column (**Cust_Name**) in the **TempTable**.

   - The value picked up from the output query column is assigned to the property P2. For example, if the customer name corresponding to purchase order **PO1234** is **John**, the value of P2 is set to John.

   - The data type of property P2 is set to **string**.

3. To update or remove a property definition, you can select the property definition in the dialog box and then click **Edit** or **Remove**. Click **OK** in the **Property Definition** dialog box and then click **Save** to save changes to the [!INCLUDE[msgflow](/Token/msgflow_md.md)].

#### To extract values from a message body using xpath

1. In **Add Property**, do the following:

   > [!NOTE]
   > This table lists only the fields required for the extract (xpath) operation. Also, depending on what you select for the **Type** drop-down list, the required fields are outlined in red and the other fields are greyed out.

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Source (Read From) <br /> <br />|Type <br /> <br />|Select **Xpath** from the drop-down list. <br /> <br />|
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|Specify the xpath query to extract an element or an attribute from a message. A typical xpath query looks like the following: <br /> <br />DELETED CODE <br /> <br />|
   |Source (Read From) <br /> <br />|Message Type <br /> <br />|Specifies the message type for the message from which the element or attribute value has to be extracted using the xpath query. <br /> <br />The drop-down list shows all the schemas that you have added to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. Select the schema that has the element that you want to extract. <br /> <br />|
   |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specifies the name of the property that you are defining. The value of this property is set to the value that is extracted from the message body using the xpath query. <br /> <br />|
   |Property (Write To) <br /> <br />|Data Type <br /> <br />|Specifies the data type for the property. You can select a value from the drop-down list. <br /> <br />|

2. Click **OK** in the **Add Property** dialog box.  The dialog boxes should resemble the following:

   ![](/Image/IntSvcs_Enrich_Xpath.gif)

   So what does this dialog box depict? It means that from a message type (PurchaseOrder, in this example), the [!INCLUDE[bridge](/Token/bridge_md.md)] extracts the value from the element per the given xpath query, assigns it to the property **P3**, and sets the data type of property P3 to **double**.

3. To update or remove a property definition, you can select the property definition in the dialog box and then click **Edit** or **Remove**. Click **OK** in the **Property Definition** dialog box and then click **Save** to save changes to the [!INCLUDE[msgflow](/Token/msgflow_md.md)].

### How do the Properties get Promoted?
At design-time using the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface, you can define the properties that will be promoted and the values that will get assigned to them. But the property promotion and value assignment actually happens at runtime; which is when a message flows through the [!INCLUDE[bridge](/Token/bridge_md.md)] deployed on [!INCLUDE[sb2](/Token/sb2_md.md)]. However, at runtime there could be instances when the property promotion fails due to various reasons. Use the following table to understand how and when that can occur:

|If this happens <br /> <br />|What gets promoted <br /> <br />|
|-------------------|----------------------|
|The SOAP or HTTP header you specify during design time does not exist in the actual message that is sent to the [!INCLUDE[bridge](/Token/bridge_md.md)] at runtime <br /> <br />|The property you defined at design time does not get promoted at run time; no exception is thrown. <br /> <br />|
|The XPATH query you specify during design time does not correspond to an element in the message that is sent to the [!INCLUDE[bridge](/Token/bridge_md.md)] at runtime <br /> <br />|The property you defined at design time does not get promoted at run time; no exception is thrown. <br /> <br />|
|For Lookup, if the Lookup property you specify at design time, does not exist at runtime (because it never got promoted) <br /> <br />|The property that would have been assigned a value as a result of the lookup does not get promoted; no exception is thrown. <br /> <br />|
|For Lookup, if the provider configuration you specify (which includes the connection string, table name, etc.) at design time is incorrect <br /> <br />|At runtime, an exception is thrown; no property gets promoted. No exception is thrown at design time because the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface does not do a validation of the provider configuration. **Important:** Only the user credentials are validated at design-time and if the validation is not successful, deployment fails. <br />|
|For Lookup, if the value of the Lookup property you specify at design time has no match in the provider data source ([!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table, in this case) at runtime <br /> <br />|An exception is thrown; no value gets promoted <br /> <br />|
|For Lookup, if the value of the Lookup property you specify at design time has more than one match in the provider data source ([!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table, in this case) at runtime <br /> <br />|The property is promoted and only one of the matching values from the data source is assigned as a value to the promoted property. <br /> <br />|
|For SOAP, HTTP, XPATH, and Lookup, if the data type specified for the property at design time is different from the data type of the value that the property will have at runtime <br /> <br />|Wherever the type conversion is possible, the type is converted and the property is promoted. For example, at design time you define a property as string but the value assigned to that property at runtime is 30, then the value of that property will be “30” (as a string.) <br /> <br />When type conversion is not possible, an exception is thrown, and the property does not get promoted. For example, at design time you define a property as “double” but the value assigned to that property at runtime is “John”. Because “John” cannot be stored in the property as a “double”, an exception is thrown and the property does not get promoted. <br /> <br />|

## <a name="BKMK_TwoWay_Transform"></a>Configure the Transform stage for the Request message
In this stage, you can enter the transforms to be used by the bridge. You can also enable or disable the stage.

1. Add the transforms to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md) lists the steps. Repeat this step to add any number of transforms that you need for your project.

2. Double-click the [!INCLUDE[request_response](/Token/request_response_md.md)] to open the itinerary designer.

3. Select the **Transform** stage. In **Properties**, set **IsEnabled** to **True** or **False**. If **True**, the stage uses the transforms that you enter for transforming an incoming request message. If **False**, there is no message transformation and the message is simply passed through to the next stage.

   **Additional**:

   - To include any custom code that executes *before* the message enters this stage, set the **On Enter Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

   - To include any custom code that executes *after* the message exits this stage, set the **On Exit Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

4. Within the **Transform** stage, select the **Xml Transform** activity. In **Properties**, select the ellipsis button **(…)** against the **Maps** property to open **Map Selection**.

5. From the list of maps displayed, select the maps that you want to associate with the **Transform** stage, and then select **OK**. The maps you added are now listed under **Selected Maps** on the itinerary designer.

   > [!IMPORTANT]
   > The dialog box only displays those maps for which the source schema (of the map) matches the request message schema you entered in [Enter the request schemas](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_AddSchemas) (in this topic).

   > [!NOTE]
   > If the **IsEnabled** property is set to True on the Transform stage and you do not specify a map as part of the **Xml Transform** activity, the [!INCLUDE[bridge](/Token/bridge_md.md)] does not thrown an error; neither while configuring the bridge (design-time) nor while processing the message (run-time).

   You can add or remove a map by clicking the ellipsis button **(…)** against the **Map** property.

6. Click **Save**.

## <a name="BKMK_TwoWay_EnrichPostTrans"></a>Configure the Enrich Stage (post- Transform) for the Request message
Configuring the **Enrich** stage after a transform stage is identical to configuring an Enrich stage before a transform stage. See [Configure the Enrich Stage (and its Properties) for the Request message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Enrich) (in this topic). The only thing to consider while configuring a post-transform Enrich stage is that the properties you defined in the pre-transform Enrich stage are also available in the post-transform Enrich stage. So, if you want to preserve those properties, do not create properties with the same name. If you do, the new property definition overwrites the old property definition.

The post-transform **Enrich** stage also provides two properties: **On Enter Inspector** and **On Exit Inspector**. These properties are used to include custom code as part of the bridge processing. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

## <a name="BKMK_TwoWay_EnrichResp"></a>Configure the Enrich Stage for the Response Message
The Enrich stage in the response path of an [!INCLUDE[request_response](/Token/request_response_md.md)] is used to promote properties on the response message that is received from the message receiver and has to be sent back to the message sender. The procedure for configuring an Enrich stage in the response path of an [!INCLUDE[request_response](/Token/request_response_md.md)] is identical to configuring an Enrich stage for the request message. See [Configure the Enrich Stage (and its Properties) for the Request message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Enrich). Note that the properties you promoted in all the previous Enrich stages within an [!INCLUDE[request_response](/Token/request_response_md.md)] are available as part of this Enrich stage.

The **Enrich** stage for the response message also provides two properties: **On Enter Inspector** and **On Exit Inspector**. These properties are used to include custom code as part of the bridge processing. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

## <a name="BKMK_TwoWay_TransformResp"></a>Configure the Transform Stage for the Response Message
The Transform stage in the response path of an [!INCLUDE[request_response](/Token/request_response_md.md)] is used to transform the response message that is received from the message receiver to a format that conforms to the schema of the message sender. The procedure for configuring a Transform stage in the response path of an [!INCLUDE[request_response](/Token/request_response_md.md)] is identical to configuring a Transform stage in a request message. See [Configure the Transform stage for the Request message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_Transform). Note that only those maps are available for selection whose destination schema (of the map) matches the response message schema you specified in [Enter the request schemas](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_AddSchemas) (in this topic).

The **Transform** stage for the response message also provides two properties: **On Enter Inspector** and **On Exit Inspector**. These properties are used to include custom code as part of the bridge processing. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

## <a name="BKMK_TwoWay_EnrichPostResp"></a>Configure the Enrich Stage (post-Transform) for the Response Message
The post-transform Enrich stage in the response path of an [!INCLUDE[request_response](/Token/request_response_md.md)] is used to promote properties on the transformed response message that is received from the message receiver and has to be sent back to the message sender. The procedure for configuring a post-transform Enrich stage in the response path of an [!INCLUDE[request_response](/Token/request_response_md.md)] is identical to configuring an Enrich stage in request message. See [Configure the Enrich Stage (post- Transform) for the Request message](/Topic/Create_an_XML_Request-Reply_Bridge.md#BKMK_TwoWay_EnrichPostTrans) (in this topic). Note that the properties you promoted in all the previous Enrich stages within an [!INCLUDE[request_response](/Token/request_response_md.md)] are available as part of this Enrich stage.

The post-transform **Enrich** stage of the response message also provides two properties: **On Enter Inspector** and **On Exit Inspector**. These properties are used to include custom code as part of the bridge processing. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

## <a name="BKMK_TwoWay_Reply"></a>Configure the Reply Action Before Routing the Response Message
While **Reply Action** is technically not a ‘stage’ in an [!INCLUDE[request_response](/Token/request_response_md.md)], it plays a key role in ensuring that any protocol mismatches between the message sender and message receiver are bridged right before the response message is finally sent back to the message sender. See [Reply Action](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md#BKMK_Send).

This section lists the steps on how to configure a Reply Action.

1. Double-click the [!INCLUDE[request_response](/Token/request_response_md.md)] to open the itinerary designer.

2. Select the **Send Reply** box. In **Properties**, set the **IsEnabled** property to **True** or **False** to determine whether you want to configure a reply action before sending the response message back to the message sender.

3. Click the **Reply Action** activity within the **Send Reply** box. In **Properties**, select the ellipsis button **(…)** against the **Reply Action** property to open the **Reply Actions** dialog box.

4. In **Reply Actions**, select **Add** to open the **Add Reply Action** dialog box. In **Add Reply Action**, do the following:

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Property (Read From) <br /> <br />|Property Name <br /> <br />|Lists all the properties that have been defined in all the previous four Enrich stages in the [!INCLUDE[request_response](/Token/request_response_md.md)]. When you select a property, you specify that the value of the selected properties be assigned to the relevant message header of the outgoing response message. <br /> <br />|
   |Property (Read From) <br /> <br />|Expression <br /> <br />|Use this option to provide an expression, the resultant value of which is passed on to the relevant message header of the outgoing response message. You can also use this option to specify a constant value that is assigned to a message header. Some example expressions are: <br /> <br /><ul><li>P1 + P2, where P1 and P2 are two properties that are already defined in any of the four previous Enrich stages </li><li>'Fabrikam', is a string constant **Important:**    You must always specify the value for an expression within single quotes. </li> </ul> **Important:** You can either choose the **Property Name** option or the **Expression** option. These options are mutually exclusive. <br />|
   |Destination (Write To) <br /> <br />|Type <br /> <br />|Specify the message type (SOAP or HTTP), the headers of which would be assigned the value that you specified earlier. <br /> <br />|
   |Destination (Write To) <br /> <br />|SOAP Header Namespace (only if the **Type** is set to **SOAP**) <br /> <br />|Specify the namespace of the custom SOAP header to which the value will be assigned. **Important:** This field is greyed out if you select a standard header from the **Identifier** drop-down list. You may choose to enter namespace only for custom SOAP headers.This field is greyed out also if the **Type** is set to **HTTP**. <br />|
   |Destination (Write To) <br /> <br />|Identifier <br /> <br />|Specifies the name of message header property to which the value will be assigned. <br /> <br />You can also specify custom headers here. For SOAP message type, the drop-down lists the four standard identifiers. For HTTP message type, because there’s a huge list of standard headers, the drop-down does not list any headers. For both SOAP and HTTP message types, you can list a custom header whose value you want to assign to another property. <br /> <br />|

5. Click **OK** in the **Add Reply Action** dialog box. The dialog boxes should now resemble the following:

   ![](/Image/IntSvcs_SendAction.gif)

   So what does this dialog box depict? It means that the [!INCLUDE[bridge](/Token/bridge_md.md)] uses the value of property P1 (already defined in one of the previous Enrich stages) and assigns it to the custom SOAP header, **PONumber** with namespace `http://schemas.microsoft.com/integration/promotedpropertiesinfo` and then sends the response message back to the message sender.

6. To update or remove a reply action, you can select it in the dialog box and then click **Edit** or **Remove**. Click **OK** in the **Reply Actions** dialog box and then click **Save** to save changes to the [!INCLUDE[msgflow](/Token/msgflow_md.md)].

## Next
The [!INCLUDE[request_response](/Token/request_response_md.md)] is configured. You can now connect the [!INCLUDE[bridge](/Token/bridge_md.md)] to a Line-of-Business system, route messages, and/or deploy the [!INCLUDE[bridge](/Token/bridge_md.md)]:

[Connect to LOB systems from a BizTalk Services Project](/Topic/Connect_to_LOB_systems_from_a_BizTalk_Services_Project.md)

[Routing Messages from Bridges to Destinations in the BizTalk Service Project](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md)

[Deploying and Refreshing the BizTalk Services Project](/Topic/Deploying_and_Refreshing_the_BizTalk_Services_Project.md)

## See Also
[Create an XML One-Way Bridge](/Topic/Create_an_XML_One-Way_Bridge.md)

