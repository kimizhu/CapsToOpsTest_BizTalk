---
description: na
keywords: na
pagetitle: Create an XML One-Way Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45edc54c-7910-46dd-bc35-7e954dd1cf94
---
# Create an XML One-Way Bridge
This section lists the steps create an [!INCLUDE[one-way](/Token/one-way_md.md)] in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]s have different stages. In this topic:

1. [Add the Bridge to the BizTalk Services project](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_AddOneWay)

2. [Enter the request schemas](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_AddSchemas) for the XML messages that are processed by the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)].

3. [Configure the Decode Stage](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_Decode)

4. [Configure the Validate stage](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_Validate)

5. [Configure the Enrich Stage and its Properties](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_Enrich)

6. [Configure the Transform stage](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_Transform)

7. [Configure the Enrich Stage (post- Transform)](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_EnrichPostTrans)

8. [Configure the Encode stage](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_Encode)

## <a name="BKMK_AddOneWay"></a>Add the Bridge to the BizTalk Services project

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md) lists the steps.

2. Right-click anywhere on the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area and select **Properties**. In **BizTalk Service URL**, enter your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL.

3. From the **Toolbox**, drag and drop the **[!INCLUDE[one-way](/Token/one-way_md.md)]** to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] design area. A *.BridgeConfig* file is added to the solution.

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

## <a name="BKMK_OneWay_AddSchemas"></a>Enter the request schemas
A single [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] can have multiple bridges and multiple schemas. For ease of use and to save on processing time, you can associate schemas with bridges. In other words, you can require that a specific bridge can only process messages that conform to a specific schema or a set of schemas. This section lists the steps to create this association.

1. Add the schemas to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md) lists the steps. Repeat this step to add any number of schemas that you need for your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

2. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] to open the itinerary designer.

   > [!NOTE]
   > The itinerary designer is a read-only area. You cannot add or remove a stage or an activity from the itinerary designer.

3. On the [!INCLUDE[bridge](/Token/bridge_md.md)] design area in the **Message Types** box, select the add icon [ ![](/Image/IntSvcs_Bridges_Add_Icon.gif) ] to open **Message Type Picker**. In **Message Type Picker**:

   1. From the **Available message types** box, select the schema for the Request message.

   2. Select the right arrow icon [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ] to associate the Request schema with the [!INCLUDE[bridge](/Token/bridge_md.md)].

   3. Select **OK**. The schema that you selected is now listed under the **Message Type** box.

      **Additional**:

      - You cannot add multiple schemas at the same time. To associate more schemas with the [!INCLUDE[bridge](/Token/bridge_md.md)], repeat this step.

      - To remove a schema association with the [!INCLUDE[bridge](/Token/bridge_md.md)], select the schema from the **Message Type** box, and then press the delete icon [ ![](/Image/IntSvcs_Bridges_Delete_Icon.gif) ].

      - To replace one schema association with another, click the edit button [ ![](/Image/IntSvcs_Bridges_Edit_Icon.gif) ] to reopen **Message Type Picker**.

4. Click **Save**.

## <a name="BKMK_OneWay_Decode"></a>Configure the Decode Stage
The **Decode** stage decodes an incoming text message to an XML message and passes it on the Validate stage in the [!INCLUDE[one-way](/Token/one-way_md.md)] bridge. Unlike other stages in the bridge, the **Decode** stage does not have an **IsEnabled** property. The **IsEnabled** property for a stage defines whether the stage processes the message passing through the bridge. The **Decode** stage does not include this property because whether the message is decoded or not depends on the content type of the incoming message. If a bridge receives a message of ‘text/plain’ content type, the decode stage decodes the message and converts it to an XML message. Rest of the processing at each stage within the bridge happens on the XML message and not the flat file message. However, if a message with the any of the other content types is received by the bridge, the decode stage is not activated and the message is simply passed over to the next stage.

The **Decode** stage does provide two properties, the **On Enter Inspector** and **On Exit Inspector**. These properties are used to include custom code as part of the bridge processing. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

## <a name="BKMK_OneWay_Validate"></a>Configure the Validate stage
In the **Validate** stage, you can enter whether the stage does any schema validation on the incoming request message and whether the validation warnings can be propagated back to the client as exceptions.

1. Double-click the [!INCLUDE[bridge](/Token/bridge_md.md)] to open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design area.

2. Select the **Validate** stage. In **Properties**, set **IsEnabled** to **True** or **False**. When **True**, the stage validates the incoming request message against the schemas you previously added. If **False**, there is no schema validation and the message is simply passed through to the next stage.

   **Additional**:

   - To include any custom code that executes *before* the message enters the **Validate** stage, set the **On Enter Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

   - To include any custom code that executes *after* the message exits the **Validate** stage, set the **On Exit Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

3. Select the **Xml Validate** activity. In **Properties**, set **Report Warnings As Errors** property to **True** or **False**. When **True**, the [!INCLUDE[bridge](/Token/bridge_md.md)] reports any warnings as errors encountered during XML validation against a schema and returns them back to the client that sent the request message. A validation warning is thrown as an exception and the validation fails. See [Validation and the Schema Object Model](http://msdn.microsoft.com/library/aa310912%28v=VS.71%29.aspx) to understand the warnings and errors in XML schema validation.

4. Click **Save**.

## <a name="BKMK_OneWay_Enrich"></a>Configure the Enrich Stage and its Properties
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

1. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] to open the itinerary designer.

2. Select the **Enrich** stage. In **Properties**, set the **IsEnabled** property to **True** or **False**.

   > [!NOTE]
   > When **True** and there is no property defined, then the [!INCLUDE[bridge](/Token/bridge_md.md)] does not throw an error when configuring the [!INCLUDE[bridge](/Token/bridge_md.md)] (design-time) nor when processing the message (run-time).

   **Additional**:

   - To include any custom code that executes *before* the message enters this stage, set the **On Enter Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

   - To include any custom code that executes *after* the message exits this stage, set the **On Exit Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

3. Within the **Enrich** stage, select the **Enrich** activity. In **Properties**, select the ellipsis button **(…)** against the **Property Definition** property to open **Property Definitions**.

4. In **Property Definitions**, select **Add**. In **Add Property**, you can use values from various sources and include them in the message as properties. These properties and their values can then be used later for other processing tasks, like routing messages to different destinations based on property values (See [The Routing Action](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md#BKMK_RoutingAction). The following table lists the different sources and ways to add properties to the message:

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

   So what does this screen capture depict? It means that if the incoming message is a SOAP message with a SOAP header name as **PONumber** and header namespace as http://schemas.microsoft.com/integration/promotedpropertiesinfo, then a **P1** with data type **string** is created and the value of header is assigned to this property.

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
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|From the drop-down list, select an already configured provider <br /> <br />If you haven’t already configured a provider, then configure one: <br /> <br /><ol><li>From the **Identifier** drop-down list, select **Configure New**. </li><li>In the **Provider Configuration** dialog box, specify the following values: <br /> <br />   **Provider Name** <br /> <br />   Specify a name for the provider <br /> <br />   **Connection String** <br /> <br />   Specify a valid connection string to connect to a [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table <br /> <br />   **Table Name** <br /> <br />   Specify the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table name from which you want to do a data lookup <br /> <br />   **Query In Column** <br /> <br />   Specify a column name in the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table, the values of which are used as the input query for performing the data lookup <br /> <br />   **Query Out Column** <br /> <br />   Specify a column name in the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table, the value is the output value that is eventually assigned to the looked up property. </li><li>Click **OK** to add the provider configuration. </li> </ol>|
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
   |Message Type <br /> <br />|Specifies the message type for the message from which the element or attribute value has to be extracted using the xpath query. <br /> <br />The drop-down list shows all the schemas that you have added to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. Select the schema that has the element that you want to extract. <br /> <br />|
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

## <a name="BKMK_OneWay_Transform"></a>Configure the Transform stage
In this stage, you can enter the transforms to be used by the bridge. You can also enable or disable the stage.

1. Add the transforms to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md) lists the steps. Repeat this step to add any number of transforms that you need for your project.

2. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] to open the itinerary designer.

3. Select the **Transform** stage. In **Properties**, set **IsEnabled** to **True** or **False**. If **True**, the stage uses the transforms that you enter for transforming an incoming request message. If **False**, there is no message transformation and the message is simply passed through to the next stage.

   **Additional**:

   - To include any custom code that executes *before* the message enters this stage, set the **On Enter Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

   - To include any custom code that executes *after* the message exits this stage, set the **On Exit Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

4. Within the **Transform** stage, select the **Xml Transform** activity. In **Properties**, select the ellipsis button **(…)** against the **Maps** property to open **Map Selection**.

5. From the list of maps displayed, select the maps that you want to associate with the **Transform** stage, and then select **OK**. The maps you added are now listed under **Selected Maps** on the itinerary designer.

   > [!IMPORTANT]
   > The dialog box only displays those maps for which the source schema (of the map) matches the request message schema you entered in [Enter the request schemas](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_AddSchemas) (in this topic).

   > [!NOTE]
   > If the **IsEnabled** property is set to True on the Transform stage and you do not specify a map as part of the **Xml Transform** activity, the [!INCLUDE[bridge](/Token/bridge_md.md)] does not thrown an error; neither while configuring the bridge (design-time) nor while processing the message (run-time).

   You can add or remove a map by clicking the ellipsis button **(…)** against the **Map** property.

6. Click **Save**.

## <a name="BKMK_OneWay_EnrichPostTrans"></a>Configure the Enrich Stage (post- Transform)
Configuring the **Enrich** stage after a transform stage is identical to configuring an Enrich stage before a transform stage. See [Configure the Enrich Stage and its Properties](/Topic/Create_an_XML_One-Way_Bridge.md#BKMK_OneWay_Enrich) (in this topic). The only thing to consider while configuring a post-transform Enrich stage is that the properties you defined in the pre-transform Enrich stage are also available in the post-transform Enrich stage. So, if you want to preserve those properties, do not create properties with the same name. If you do, the new property definition overwrites the old property definition.

The post-transform **Enrich** stage also provides two properties: **On Enter Inspector** and **On Exit Inspector**. These properties are used to include custom code as part of the bridge processing. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

## <a name="BKMK_OneWay_Encode"></a>Configure the Encode stage
In this stage, you can enter the flat-file schema to use for converting an XML message into a flat-file message. By the time a message reaches the **Encode** stage, it is already in the XML format. Depending on how the **Encode** stage is configured, the message is either encoded to a flat-file format or sent out as an XML message.

1. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] to open the itinerary designer.

2. Select the **Encode** stage. In **Properties**, set the **IsEnabled** property to **True** or **False**. If **True**, the stage uses the flat-file schemas that you enter for encoding the XML message to a flat-file message. If **False**, there is no encoding and the XML message is sent out from the bridge.

   **Additional**:

   - To include any custom code that executes *before* the message enters this stage, set the **On Enter Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

   - To include any custom code that executes *after* the message exits this stage, set the **On Exit Inspector** property. See [How to Include Custom Code in Bridges](/Topic/How_to_Include_Custom_Code_in_Bridges.md).

3. Within the **Encode** stage, select the **Flat File Encode** activity. In **Properties**, click the ellipsis button **(…)** against the **Flat File Schemas** property to open the **Flat File Schema Selection** dialog box.

4. From the list of flat-file schemas displayed in the dialog box, select the schemas that you want to use to encode the XML message to a flat-file message, and then click **OK**. At run time when an XML message reaches the **Flat File Encode** activity, the message type (Namespace#Root) is mapped against the flat file schemas provided as part of the activity configuration. If a match occurs, then that schema is used to convert the XML message to a flat file message. The HTTP header for the converted messages is set to “text/plain”. If a match does not occur, the XML processed is sent out by the Encode stage as-is.

   > [!NOTE]
   > If the **IsEnabled** property is set to **True** on the **Encode** stage and you do not specify a flat file schema as part of the **Flat File Encode** activity, the [!INCLUDE[bridge](/Token/bridge_md.md)] does not thrown an error; neither while configuring the bridge (design-time) nor while processing the message (run-time).

   You can add or remove a schema by clicking the ellipsis button **(…)** against the **Flat File Schemas** property.

5. Click **Save**.

## Next
The [!INCLUDE[one-way](/Token/one-way_md.md)] is configured. You can now connect the [!INCLUDE[bridge](/Token/bridge_md.md)] to a Line-of-Business system, route messages, and/or deploy the [!INCLUDE[bridge](/Token/bridge_md.md)]:

[Connect to LOB systems from a BizTalk Services Project](/Topic/Connect_to_LOB_systems_from_a_BizTalk_Services_Project.md)

[Routing Messages from Bridges to Destinations in the BizTalk Service Project](/Topic/Routing_Messages_from_Bridges_to_Destinations_in_the_BizTalk_Service_Project.md)

[Deploying and Refreshing the BizTalk Services Project](/Topic/Deploying_and_Refreshing_the_BizTalk_Services_Project.md)

## See Also
[Create an XML Request-Reply Bridge](/Topic/Create_an_XML_Request-Reply_Bridge.md)
[Create and Configure a Bridge](/Topic/Create_and_Configure_a_Bridge.md)

