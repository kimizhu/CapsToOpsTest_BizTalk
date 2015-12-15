---
description: na
keywords: na
pagetitle: Routing Messages from Bridges to Destinations in the BizTalk Service Project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 498de1a4-3427-4314-a152-8d5a7f026cc0
---
# Routing Messages from Bridges to Destinations in the BizTalk Service Project
Route messages from one component to another using routing conditions.

One of the obvious reasons for connecting various components of a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] is to route the message from one component to another. There’s another requirement though – you might need to route the message from one source component to more than one destination component based on your business logic, which can also be termed as the routing condition. When there are more than one routing conditions, you also need to set the order in which the routing conditions are honored. And finally, there can be some actions (like assigning values to message headers, adding custom headers, etc.) that you perform on the message before it finally gets routed to the destination. This topic discusses these aspects in detail and also provides instructions how to achieve these in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

This topic explains these steps using an example scenario. Assume that an XML message in the following format has to be processed using a [!INCLUDE[one-way](/Token/one-way_md.md)]:

```
<PaymentHistory xmlns:ns0="http://Integration.PipelineChaining">
  <BaseData>
    <Amount>10.4</Amount> 
    <CurrencyCode>CurrencyCode_0</CurrencyCode> 
    <EntryDate>1999-05-31</EntryDate> 
    <EntryTime>13:20:00.000-05:00</EntryTime> 
    <PaymentMode>Mode_0</PaymentMode> 
    <StatusCode>StatusCode_0</StatusCode> 
    <PurposeCode>PurposeCode_0</PurposeCode> 
  </BaseData>
</PaymentHistory>
```
The business logic is such that if the payment mode is a credit card, the message must be routed to a one-way external service; if the mode is cash, the message must be routed to a one-way relay endpoint; and if the mode is neither of these, it must be routed to a [!INCLUDE[sb2](/Token/sb2_md.md)] queue.

## <a name="BKMK_Connect"></a>The Routing Destination
This is fairly straightforward. You must define the route destination where the incoming message gets routed to after being processed by the [!INCLUDE[bridge](/Token/bridge_md.md)].  There are some considerations regarding where a message from an [!INCLUDE[one-way](/Token/one-way_md.md)] or an [!INCLUDE[request_response](/Token/request_response_md.md)] can be routed to. For more information about these considerations, see [Constraints on Using an XML One-Way Bridge](/Topic/Message_Exchange_Patterns_for_Bridges.md#BKMK_ConstOneWay) and [Constraints on Using an XML Request Reply Bridge](/Topic/Message_Exchange_Patterns_for_Bridges.md#BKMK_ConstTwoWay).

The following procedure describes how to connect two components of a message flow.

#### To connect two components

1. Create a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], as described in [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

2. Add components to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], as described in various topics under [Create Rich Messaging Endpoints on Azure](/Topic/Create_Rich_Messaging_Endpoints_on_Azure.md).

3. Select **Connector** under the **Bridges** category on the **Toolbox**.

4. Take the mouse pointer to the right-end of the component (marked by a red dot when you move the cursor over the component) that acta as the source of the message. The mouse pointer changes to show a small “**S**” sign denoting that this component adds the source of the message. Click and hold the mouse at the dot, drag it to the left end of the target component (at this point the cursor changes again to show a small “**T**” denoting the target), and then release the mouse. The two components are now connected. Note that you can connect one source component to more than one target component.

   > [!NOTE]
   > For the current milestone, a message flow must always start with either a [!INCLUDE[one-way](/Token/one-way_md.md)] or a [!INCLUDE[request_response](/Token/request_response_md.md)]. After that, you can route the message to any component, as long as you adhere to the constraints. The constraints are listed at [Constraints on Using an XML One-Way Bridge](/Topic/Message_Exchange_Patterns_for_Bridges.md#BKMK_ConstOneWay) and [Constraints on Using an XML Request Reply Bridge](/Topic/Message_Exchange_Patterns_for_Bridges.md#BKMK_ConstTwoWay).

   Going by the example scenario, you must connect the [!INCLUDE[one-way](/Token/one-way_md.md)] to a one-way external service, a one-way relay endpoint, and a [!INCLUDE[sb2](/Token/sb2_md.md)] queue.

## <a name="BKMK_Filter"></a>The Routing Condition
Apart from connecting two components, the other important aspect of routing is to route the message from one source component to more than one destination component based on your business logic.

Going by the example scenario explained above, the routing condition must be based on the mode of payment, which is denoted by the **PaymentMode** element in the XML message. To implement this business logic in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], we need to create routing filters for each condition. The following procedure describes how to do so.

> [!NOTE]
> Before you start creating filters, ensure that you have created all the three Connectors (as described in the previous procedure). Also, you must have created a property (e.g.  *PaymentMode*) in the **Enrich** stage of a bridge to extract the value of the **PaymentMode** element in the XML message.

The following procedure describes how to set the routing conditions in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

#### To set filters on the routing connectors

1. Right-click the route connector between [!INCLUDE[one-way](/Token/one-way_md.md)] and the one-way external service, and then click **Properties**. In the Properties pane, for the **Filter Condition** property, click the ellipsis **(…)** button to the open the **Route Filter Configuration** dialog box.

2. In the dialog box, select the **Filter** option, and then enter the following filter string:

   ```
   PaymentMode='credit_card'
   ```
   > [!NOTE]
   > You must use standard SQL 92 syntax for filter expressions.

   Note that **PaymentMode** is the property that you must have entered for extraction in the Enrich stage and this filter condition (which is entered on the connector between [!INCLUDE[one-way](/Token/one-way_md.md)] and one-way external service) specifies that the message is sent to the one-way external service, if this filter condition is met.

   Click **OK** to save the changes and exit.

3. Similarly, for the connector between [!INCLUDE[one-way](/Token/one-way_md.md)] and one-way relay endpoint, enter the filter string as:

   ```
   PaymentMode='cash'
   ```

4. If the payment mode is neither cash nor credit card, the message should be routed to a [!INCLUDE[sb2](/Token/sb2_md.md)] queue. To achieve that in your message flow, for the connector between [!INCLUDE[one-way](/Token/one-way_md.md)] and [!INCLUDE[sb2](/Token/sb2_md.md)] queue, you must open the **Route Filter Configuration** dialog box, and then select **Match All**. This specifies that if neither of the filter conditions matches, this filter condition is honored and the message is routed to a [!INCLUDE[sb2](/Token/sb2_md.md)] queue.

## <a name="BKMK_Order"></a>The Routing Order
In the previous section we set the filters on the route connectors to ensure that the right messages get routed to the right components of a message flow. However, the order of routing is equally important. For example, going by the scenario we discussed earlier, if a message that has **PaymentMode** set to **credit_card** is routed to the filter condition that has **Match All** set, it is routed to a [!INCLUDE[sb2](/Token/sb2_md.md)] queue instead of the one-way external service endpoint. So, according to the business logic, the **Match All** condition should be honored last. You can do so by setting the order in which the filter conditions must be honored.

#### To set the order in which routing connectors are honored

1. Right-click the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] ([!INCLUDE[one-way](/Token/one-way_md.md)] or [!INCLUDE[request_response](/Token/request_response_md.md)]) and select **Properties**. In the Properties pane, click the ellipsis **(…)** button against the **Route Ordering Table** property.

2. The **Route Ordering Table** dialog box displays the default order of honoring the route filters. This default order is the order in which you created the route connectors. To re-order the route filters, select a route filter and then use the up and down arrow buttons to arrange them in the right order. You must repeat this step for all the route filters until you have the correct route order that you want.

3. Click **OK** to save the changes and exit.

## <a name="BKMK_RoutingAction"></a>The Routing Action
You might want to add some custom message headers or assign values to standard message headers before sending the message to the message receiver. You can do so using Route action. For more information, see [Route Action](/Topic/Route_and_Reply_Actions__Bridging_Protocol_Mismatch.md#BKMK_Route).

To continue with the example used above, assume that the message has to be sent to the one-way external service with a custom SOAP header (**CustomerName**) and a value.

#### To configure the Route action

1. Right-click the route connector between the bridge and the one-way external service, and then click **Properties**. In the Properties pane, for the **Route Action** property, click the ellipsis **(…)** button to the open the **Route Actions** dialog box.

2. In the **Route Actions** dialog box, click **Add** to open the **Add Route Action** dialog box. In the **Add Route Action** dialog box, do the following:

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Property (Read From) <br /> <br />|Property Name <br /> <br />|Lists all the properties that have been defined in the previous two Enrich stages in the [!INCLUDE[request_response](/Token/request_response_md.md)]. When you select a property here, you specify that the value of the selected property must be assigned to the relevant message header of the outgoing message. <br /> <br />|
   |Property (Read From) <br /> <br />|Expression <br /> <br />|Use this option to provide an expression, the resultant value of which is passed on to the relevant message header of the outgoing message. You can also use this option to enter a constant value that is assigned to a message header. Some example expressions are: <br /> <br /><ul><li>P1 + P2, where P1 and P2 are two properties that are already defined in any of the previous two Enrich stages </li><li>'Fabrikam', is a string constant **Important:**    You must always enter the value for an expression within single quotes. </li> </ul> **Important:** You can either choose the **Property Name** option or the **Expression** option. These options are mutually exclusive. <br />|
   |Destination (Write To) <br /> <br />|Type <br /> <br />|Enter the message type of the outgoing message, the header of which would be assigned the value that you entered earlier. <br /> <br />Depending on the message destination, the values available in the drop-down change. <br /> <br /><ul><li>If you are routing to an external service or a relay endpoint (one-way or two-way), the values available from the drop-down list are **SOAP** and **HTTP**. </li><li>If you are routing to a queue or a topic, the values available from the drop-down list are **SOAP** and **Brokered**. </li><li>If you are routing to an FTP destination, the value available from the drop-down is **FTP**. </li><li>If you are routing to an SFTP destination, the value available from the drop-down is **SFTP**. </li><li>If you are routing to an Azure blob, the value available from the drop-down is **Azure Blob**. </li> </ul>|
   |Destination (Write To) <br /> <br />|SOAP Header Namespace (only if the **Type** is set to **SOAP**) <br /> <br />|Enter the namespace of the custom SOAP header to which the value is assigned. **Important:** This field is greyed out if you select a standard header from the **Identifier** drop-down list. You are required to enter a namespace only for custom SOAP headers.This field is greyed out also if the **Type** is set to **HTTP** or **Brokered**. <br />|
   |Destination (Write To) <br /> <br />|Identifier <br /> <br />|Enter the name of message header property to which the value is assigned. <br /> <br />You can also enter custom headers here. For SOAP message type, the drop-down lists the four standard identifiers. For HTTP message type, because there’s a huge list of standard headers, the drop-down does not list any headers. For both SOAP and HTTP message types, you can list a custom header whose value you want to assign to another property. <br /> <br />For other destination types such as FTP, SFTP, and [!INCLUDE[azure_2](/Token/azure_2_md.md)] blobs, you can select the message headers to which the property value must be written. <br /> <br />Going with the example we took earlier, you must set this to **CustomerName** because that is the custom header name you must include in the outgoing message. <br /> <br />|

3. Click **OK** in the **Add Route Action** dialog box. The dialog boxes should now resemble the following:

   ![](/Image/IntSvcs_Route_Action.gif)

   So what does this dialog box depict? It means that the [!INCLUDE[bridge](/Token/bridge_md.md)] would use the value of property P1 (already defined in one of the previous Enrich stages) and assign it to the custom SOAP header, **CustomerName** with namespace `http://schemas.microsoft.com/integration/promotedpropertiesinfo` and then send it out to the message receiver.

   > [!IMPORTANT]
   > If you create two route actions on the same route connector that point to the same destination using two different properties, for example P1 and P2, you do not get a build error. The last route action overrides the previously defined route actions. In this example, the route action for the property P2 is honored.

4. To update or remove a route action, you can select it in the dialog box and then click **Edit** or **Remove** respectively. Click **OK** in the **Route Actions** dialog box and then click **Save** to save changes to a [!INCLUDE[msgflow](/Token/msgflow_md.md)].

## See Also
[How Messages get Routed from a Bridge](/Topic/How_Messages_get_Routed_from_a_Bridge.md)

