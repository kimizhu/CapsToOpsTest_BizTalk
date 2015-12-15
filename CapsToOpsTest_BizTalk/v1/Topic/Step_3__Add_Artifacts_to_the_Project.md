---
description: na
keywords: na
pagetitle: Step 3: Add Artifacts to the Project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1442290a-8fca-42c6-97c4-7e3bb4e55344
---
# Step 3: Add Artifacts to the Project
As per the business scenario, Northwind Traders receive the insurance quotes in more than one XML format. So, the tutorial assumes that there are two schemas in which Northwind receives insurance quotes. Both schemas are compliant with the ACORD standards. Assume the schema names to be **ACORDRq1.xsd** and **ACORDRq2.xsd**. There must be two response schemas as well that are compliant with ACORD standards, one each for each request schema. The response schemas are called **ACORDRs1.xsd** and **ACORDRs2.xsd**, respectively. Finally, per the business scenario, Northwind normalizes request messages in both the formats into a schema proprietary to Northwind, called **NorthwindSchema.xsd**. This tutorial assumes that the schemas are in the following format:

![](/Image/BridgeSvc_Schemas.gif)

> [!NOTE]
> The tutorial does not get into the details of creating these schemas.

After the schemas, the second set of artifacts required in the tutorial are [!INCLUDE[transform](/Token/transform_md.md)]s. The [!INCLUDE[transform](/Token/transform_md.md)]s map the request messages from the ACORD schema to the request message schema that is proprietary to Northwind. To start with the tutorial requires two [!INCLUDE[transform](/Token/transform_md.md)]s, one to map ACORDRq1.xsd to NorthwindSchema.xsd (let’s call this **ACORDRq1_To_Northwind.trfm**) and one to map ACORDRq2.xsd to NorthwindSchema.xsd (let’s call this **ACORDRq2_To_Northwind.trfm**). Similarly two [!INCLUDE[transform](/Token/transform_md.md)]s are required to map the response from Northwind into the response messages compliant with ACORD schema. One [!INCLUDE[transform](/Token/transform_md.md)] maps the response from Northwind to ACORDRs1.xsd (let’s call this **Northwind_To_ACORDRs1.trfm**) and the other map the response from Northwind to ACORDRs2.xsd (let’s call this **Northwind_To_ACORDRs2.xsd**).

The following illustration summarizes how [!INCLUDE[transform](/Token/transform_md.md)]s map the different schemas.

![](/Image/BridgeSvc_MapFlow.gif)

This topic demonstrates how to create these [!INCLUDE[transform](/Token/transform_md.md)]s for mapping the different source and destination schemas. The two request schemas are the same, except for the **Comments** node in the **ACORDRq2.xsd**. So, for creating [!INCLUDE[transform](/Token/transform_md.md)]s for request schemas, the following procedure only demonstrates creating one [!INCLUDE[transform](/Token/transform_md.md)] (from ACORDRq1.xsd to NorthwindSchema.xsd). You can follow the same steps to create the other [!INCLUDE[transform](/Token/transform_md.md)] as well (from ACORDRs2.xsd to NorthwindSchemas.xsd). Moreover, because the **NorthwindSchema.xsd** does not have a **Comments** node, the node in the **ACORDRq2.xsd** does not have a matching node in the destination schema and hence doesn’t require mapping.

> [!IMPORTANT]
> All the artifacts (the five schemas and the four [!INCLUDE[transform](/Token/transform_md.md)]s) used in this solution are also packaged with the **Bridges_RelayServices** sample. You can download the sample from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=252395). You can look at those artifacts as well for a better understanding. You can also add the schemas bundled with the sample to your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

### To map ACORDRq1.xsd and ACORDRq2.xsd to NorthwindSchema.xsd

1. In the **Bridges_RelayServices** solution, right-click the project, point to **Add**, and select **New Item**.

2. From **Add New Item**, select **Map**, enter **ACORDRq1_To_Northwind.trfm** for the name, and then select **Add**.

3. For the source schema, select **ACORDRq1.xsd**. For the destination schema, select **NorthwindSchema.xsd**. The elements in the following table are directly mapped to each other, simply by connecting the two nodes, without the use of any [!INCLUDE[mapop](/Token/mapop_md.md)].

   |Node in the source schema <br /> <br />|Node in the destination schema <br /> <br />|
   |-----------------------------|----------------------------------|
   |ACORDStandardVersionCd <br /> <br />|ACORDStandardVersionCd <br /> <br />|
   |RqUID <br /> <br />|RqUID <br /> <br />|
   |TransactionRequestDt <br /> <br />|TransactionRequestDt <br /> <br />|
   |CurCd <br /> <br />|CurCd <br /> <br />|
   |InsuredOrPrincipal <br /> <br />|InsuredOrPrincipal <br /> <br />|
   |QuoteAmount <br /> <br />|QuoteAmount <br /> <br />|

4. Parent node **PersPolicy** node and its child node **LOBCd** in the source schema map to the same elements in the destination schema. However, because **PersPolicy** is marked as ‘unbounded’ in the schema, it can appear more than once in the XML request message. So, the [!INCLUDE[transform](/Token/transform_md.md)] must have a way to map each iteration of the **PersPolicy** node and its child node (**LOBCd**) to the relevant nodes in the destination schema. The **MapEach Loop** operation does just that. When you connect two elements in the source and destination schema by using a **MapEach Loop** operation, every occurrence of the element in the source schema is mapped to the relevant occurrence of the element in the target schema. Needless to say that the relevant node in the destination schema must also be marked as ‘unbounded’, as is the case in this tutorial where the node in the destination schema is also marked as unbounded.

   Another important thing to understand about **MapEach Loop**, and other loop operations in general, is the concept of *scopes*. Like programming languages, you can create scopes within [!INCLUDE[transform](/Token/transform_md.md)]s as well. All the relationships (simple mappings or ones that involve [!INCLUDE[mapop](/Token/mapop_md.md)]s) defined within a scope are specific to the scope. But why discuss scopes when all that’s required is a **MapEach Loop** operation? That’s because adding a **MapEach Loop** operation, by default creates a new scope. So, perform the following series of steps to add the **PersPolicy** and **LOBCd** nodes to the relevant elements in the destination schemas:

   - Map **PersPolicy** nodes in the source and destination schema by using a **MapEach Loop**[!INCLUDE[mapop](/Token/mapop_md.md)]. Adding a MapEach Loop also creates a scope.

   - Within the scope, map the **LOBCd** nodes in the source and destination schemas.

   - Close the scope.

   1. Drag and drop the **MapEach Loop**[!INCLUDE[mapop](/Token/mapop_md.md)] to the [!INCLUDE[transform](/Token/transform_md.md)] design surface. Notice that the scope is created in the **MapEach Loop** operation box, as this icon denotes (![](/Image/BtsSvc_Relay_Map_SetScope.gif)).

   2. Connect the **PersPolicy** node in the source schema to the **MapEach Loop**[!INCLUDE[mapop](/Token/mapop_md.md)]. Similarly, connect the **PersPolicy** node in the destination schema to the same [!INCLUDE[mapop](/Token/mapop_md.md)].

   3. Map the **LOBCd** nodes in the source and destination schema. Notice that the link snaps to go ‘through’ the **MapEach Loop** operation, irrespective of how you link it. That’s because the actions are still being performed in the scope that the **MapEach Loop** operation created.

   4. Close the scope by selecting the icon (![](/Image/BtsSvc_Relay_Map_SetScope.gif)). The icon now changes to the following: ![](/Image/BtsSvc_Relay_Map_UnsetScope.gif).

5. Repeat step 4 to map the **PersAutoLoanBusiness** node, along with its child node, in the source and destination schemas. The final mapping resembles the following:

   ![](/Image/BridgesSvc_Map1.gif)

   Save changes to the project.

   > [!NOTE]
   > Follow this procedure to create the [!INCLUDE[transform](/Token/transform_md.md)]**ACORDRq2_To_Northwind.trfm**.

### To map NorthwindSchema.xsd to ACORDRs1.xsd

1. In the **Bridges_Services** solution, right-click the project, point to **Add**, and select **New Item**.

2. From **Add New Item**, select **Map**, enter **Northwind_To_ACORDRs1.trfm** for the name, and then select **Add**.

3. For the source schema, select **NorthwindSchema.xsd**. For the destination schema, select **ACORDRs1.xsd**. The elements in the following table are directly mapped to each other, simply by connecting the two nodes, without the use of any [!INCLUDE[mapop](/Token/mapop_md.md)].

   |Node in the source schema <br /> <br />|Node in the destination schema <br /> <br />|
   |-----------------------------|----------------------------------|
   |ACORDStandardVersionCd <br /> <br />|ACORDStandardVersionCd <br /> <br />|
   |RqUID <br /> <br />|RqUID <br /> <br />|
   |TransactionRequestDt <br /> <br />|TransactionRequestDt <br /> <br />|

4. The destination schema, **ACORDRs1.xsd** has a node called **MsgStatusCd**. The **MsgStatusCd** node must contain the value of the **MsgStatus** SOAP header that is set on the response message by the relay services. The typical way to do add this header with the value would be to:

   - Create a property, for example **MsgStatus**, as part of the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration (**Enrich** stage) to extract the value from the response message header. The tutorial demonstrates how to create this property in the subsequent steps, as described at [To extract and promote properties in the pre-transform Enrich stage](/Topic/Step_4_b):%20Configure%20the%20Response%20Bridge.md#BKMK_ResP_Enrich).

   - Use the **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] to pass the value from the **MsgStatus** property to the **MsgStatusCd** node in the response schema.

   Even though the **MsgStatus** property is not yet created as part of the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration, one can still go ahead and use the [!INCLUDE[mapop](/Token/mapop_md.md)]. The only thing to ensure would be that the same property name is used (in this case **MsgStatus**) while configuring the Enrich stage in the [!INCLUDE[bridge](/Token/bridge_md.md)].

   1. Drag and drop a **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] on the map designer surface. Double-click the [!INCLUDE[mapop](/Token/mapop_md.md)] and in the dialog box, for the **Property** name field, enter **MsgStatus**, and then select **OK**.

   2. Connect the **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] to the **MsgStatusCd** node in the destination schema. The final map resembles the following:

      ![](/Image/BridgesSvc_Map2.gif)

5. Save changes to the project.

### To map NorthwindSchema.xsd to ACORDRs2.xsd

1. In the **Bridges_Services** solution, right-click the project, point to **Add**, and select **New Item**.

2. From **Add New Item**, select **Map**, enter **Northwind_To_ACORDRs2.trfm** for the name, and then select **Add**.

3. For the source schema, select **NorthwindSchema.xsd**. For the destination schema, select **ACORDRs2.xsd**. The elements in the following table are directly mapped to each other, simply by connecting the two nodes, without the use of any [!INCLUDE[mapop](/Token/mapop_md.md)].

   |Node in the source schema <br /> <br />|Node in the destination schema <br /> <br />|
   |-----------------------------|----------------------------------|
   |ACORDStandardVersionCd <br /> <br />|ACORDStandardVersionCd <br /> <br />|
   |RqUID <br /> <br />|RqUID <br /> <br />|
   |TransactionRequestDt <br /> <br />|TransactionRequestDt <br /> <br />|

4. Repeat step 4 in the procedure [To map NorthwindSchema.xsd to ACORDRs1.xsd](/Topic/Step_3__Add_Artifacts_to_the_Project.md#BKMK_TransformRes1) to map a value to the **MsgStatusCd** node in the destination schema.

5. Just like **ACORDRq2.xsd**, **ACORDRs2.xsd** has a node called **Comments**. How to get the value for this node? Unlike **MsgStatus**, it’s not a value that is present in the response message header. But it’s a value that is present in the request message and can be extracted from the request message itself. To set the value for **Comments** property in the response message, do the following:

   - Create a property, for example **Comments**, as part of the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration (**Enrich** stage) to extract the value from **Comments** element in the request message. The tutorial demonstrates how to create this property in the subsequent steps, as described at [To extract and promote properties in the pre-transform Enrich stage](/Topic/Step_4_a):%20Configure%20the%20Request%20Bridge.md#BKMK_ReqP_Enrich).

   - Use the **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] to pass the value from the **Comments** property to the **Comments** node in the response schema.

   Even though the **Comments** property is not yet created as part of the [!INCLUDE[bridge](/Token/bridge_md.md)] configuration, one can still go ahead and use the [!INCLUDE[mapop](/Token/mapop_md.md)]. The only thing to ensure would be that the same property name is used (in this case **Comments**) while configuring the Enrich stage in the [!INCLUDE[bridge](/Token/bridge_md.md)].

   1. Drag and drop a **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] on the [!INCLUDE[transform](/Token/transform_md.md)] design surface. Double-click the [!INCLUDE[mapop](/Token/mapop_md.md)] and in the dialog box, for the **Property** name field, enter **Comments**, and then select **OK**.

   2. Connect the **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] to the **Comments** node in the destination schema. The final [!INCLUDE[transform](/Token/transform_md.md)] resembles the following:

      ![](/Image/BridgesSvc_Map3.gif)

6. Save changes to the project.

## See Also
[Tutorial: Using BizTalk Service Bridges to Send and Receive Messages from Service Bus Relay Service](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md)

