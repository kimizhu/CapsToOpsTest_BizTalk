---
description: na
keywords: na
pagetitle: Step 6: Configure a One-Way Bridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8cffcf3-2815-4e19-84b5-5b75d8b3f0c4
---
# Step 6: Configure a One-Way Bridge
This step demonstrates how to configure a one-way bridge that processes incoming flat-file messages, looks up information from a [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)], includes that information in the original message, and then routes the message to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] endpoint. To configure the bridge to perform these tasks, you must perform the following steps:

- Add the schema of the incoming flat file message to the bridge configuration to ensure that the bridge processes all incoming message that validate against that schema. You create that schema earlier, as described in the topic [Step 3: Generate the Schema for the Flat File Message](/Topic/Step_3__Generate_the_Schema_for_the_Flat_File_Message.md).

- Define properties that can be used to track the message as it gets processed by the bridge.

- Look up an external [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table to enrich the incoming message and add more information about the insurance claims before the data is finally written to the on-premises SQL Server database.

## Specify the Schema for the Incoming Flat File Message
This section demonstrates how to add a bridge to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and configure it to validate flat file messages of a specific schema.

#### To specify the schema

1. In the **FlatFile_Bridge** project, double-click the **MessageFlowItinerary.bcs** file to open the bridge configuration surface.

2. From the **Toolbox**, drag-and-drop the **[!INCLUDE[one-way](/Token/one-way_md.md)]** component to the bridge design surface. This adds a .BridgeConfig file to the solution.

3. Right-click the **[!INCLUDE[one-way](/Token/one-way_md.md)]**, select **Properties**, set the bridge entity name to **ClaimsBridge** and the relative address of the bridge to **ClaimsProcessing**. With this configuration, the endpoint where the bridge gets deployed is `https://mybiztalkservicename.biztalk.windows.net/default/ClaimsProcessing`.

4. Double-click the [!INCLUDE[one-way](/Token/one-way_md.md)] component to open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] design surface. You can now specify the type of message that the bridge can process. To specify the message type, on the [!INCLUDE[one-way](/Token/one-way_md.md)] design surface, within the **Message Types** box, click the add icon [ ![](/Image/IntSvcs_Bridges_Add_Icon.gif) ] to open the **Message Type Picker** dialog box.

5. In the **Message Type Picker** dialog box, from the **Available message types** box, select the schema for the request message and then click the RIGHT ARROW icon  [ ![](/Image/IntSvcs_Bridges_Arrow_Icon.gif) ], and then click **OK**. For this tutorial, select the **SourceClaim** schema (`http://FlatFile_Bridge.InsuranceClaim`). The selected schema is listed under the **Request Message Type** box.

   > [!TIP]
   > Even though it’s out of the context of this scenario, here’s some information that can be useful. You can configure the same bridge to process flat-file as well as XML messages. This is especially helpful because you don’t need to configure two separate bridges, when your message-processing logic is essentially the same and the only thing that varies is the format of the incoming message. Just like you specified a flat-file message schema in the Message Type dialog box to process flat-file messages using the bridge, you can specify an XML message schema as the message type. For that, you must have already added that XML message schema to the project. Once you have done that, you can send either a flat-file message or an XML message and the bridge processes it through the stages you define in the bridge.

6. Save the bridge configuration.

## <a name="BKMK_Tracking"></a>Configure Tracking
By default, the bridge always tracks certain stages such as when a bridge activity faulted, when a bridge stage faulted, and so on. However, you can also ‘promote’ certain elements in the incoming message (or the message after it has been transformed) as properties within the bridge, and then track the value of those properties as the message gets processed by the bridge. This section demonstrates how to promote a few properties and then configure tracking for those properties. For more information on tracking, see [Operational Tracking of Messages Processed by the Bridge](http://go.microsoft.com/fwlink/?LinkId=250919).

This tutorial provides instructions to promote two elements, **ClaimType** (in the incoming flat-file message) and **ClaimTypeDescription** (in the message schema for the Insert operation on the **Claims** table). The tutorial also includes instructions on how to track the values of these properties when the bridge processes the message.

> [!TIP]
> To promote the **ClaimType** and **ClaimTypeDescription** properties, we will use the XPath method within the bridge’s **Enrich** stage. For that you must have the XPath query string for both **ClaimType** and **ClaimTypeDescription** elements. You can get the XPath query from the schema editor. Select the schema element in the schema editor, and in the **Properties** window look for the value of the **Instance XPath** property. The value of the property is XPath query for the node.

#### To define properties and configure tracking

1. Within the pre-transform **Enrich** stage, select the **Enrich** activity, and then from the **Properties** pane click the ellipsis button **(…)** against the **Properties** property to open the **Property Definitions** dialog box.

2. In the **Property Definitions** dialog box, click **Add** to open the **Add Property** dialog box. In the **Add Property** dialog box, do the following:

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Source (Read From) <br /> <br />|Type <br /> <br />|Select **XPath** from the drop-down list. <br /> <br />|
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|Specify the XPath query to extract the value of the **ClaimType** from the request schema. **Tip:** To get the Xpath query, select the **ClaimType** element in the schema editor, and in the Properties window look for the value of the **Instance XPath** property. <br />|
   |Source (Read From) <br /> <br />|Message Type <br /> <br />|Select the schema for the **SourceClaim** message. <br /> <br />|
   |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specifies the name of the property that you are defining. For this tutorial, specify **ClaimType**. <br /> <br />|
   |Property (Write To) <br /> <br />|Data Type <br /> <br />|Specifies the data type for the property. Specify **string**. <br /> <br />|
   The dialog box resembles the following:

   ![](/Image/FFBridge-PromoteXPath1.gif)

3. Click **OK** in the **Add Property** dialog box and then click **OK** in the **Property Definition** dialog box.

4. Now, within the post-transform **Enrich** stage, select the **Enrich** activity, and then from the **Properties** pane click the ellipsis button **(…)** against the **Properties** property to open the **Property Definition** dialog box.

5. In the **Property Definitions** dialog box, click **Add** to open the **Add Property** dialog box. In the **Add Property** dialog box, do the following:

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Source (Read From) <br /> <br />|Type <br /> <br />|Select **XPath** from the drop-down list. <br /> <br />|
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|Specify the XPath query to extract the value of the **ClaimTypeDescription** from the request schema. <br /> <br />|
   |Source (Read From) <br /> <br />|Message Type <br /> <br />|Select the schema for the **Insert** operation. <br /> <br />|
   |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specifies the name of the property that you are defining. For this tutorial, specify **ClaimTypeDescription**. <br /> <br />|
   |Property (Write To) <br /> <br />|Data Type <br /> <br />|Specifies the data type for the property. Specify **string**. <br /> <br />|
   The dialog box resembles the following:

   ![](/Image/FFBridge-PromoteXPath2.gif)

   Click **OK** in **Add Property** dialog box and then the **Property Definitions** dialog box.

   > [!NOTE]
   > Save changes to the bridge configuration. If you do not save the changes, the properties you promoted will not be available for tracking.

   > [!IMPORTANT]
   > If you are wondering why the **ClaimTypeDescription** property is promoted in the post-transform **Enrich** stage and not the pre-transform stage, here’s the reason behind it. The **ClaimTypeDescription** element is in the Insert message schema. At run time, the bridge transforms the flat-file message into the Insert message for SQL Server **Claims** table by using a transform that we’ll create later in this tutorial. Only after the message is transformed, the **ClaimTypeDescription** element will have any value assigned to it. So, there’s no use of tracking the property before it gets transformed and hence you promote this property in the post-transform **Enrich** stage.

6. Now that the two properties for tracking have been defined, let us configure tracking for the two properties. Right-click the bridge component, and then select **Properties**. From the **Properties** window, click the ellipsis (…) against **Track Properties**.

7. In the **Track Properties** dialog box, do the following:

   1. Select the **Track message processing events** check box to track detailed information such as when a stage starts, completes, or faults; when an activity within a stage starts, completes, or faults; whether an artifact gets retrieved, and so on.

   2. Select the **ClaimType** and **ClaimTypeDescription** properties to track. These properties are listed in the box because these were promoted in the Enrich stages.

      ![](/Image/FFBridge-ConfigTracking.gif)

      Click **OK**.

      For detailed information on what properties get tracked and how the messages get tracked, see [Tracking Messages Processed by the Bridge](/Topic/Tracking_Messages_Processed_by_the_Bridge.md).

8. Save the project.

## Configure Data Lookup
As described in the business scenario at [Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md), Humongous Insurance ‘enriches’ the incoming message by looking up an external [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] table to retrieve claim type description that maps to the value in the **ClaimType** element in the incoming flat file message received from Northwind Insurance. This section demonstrates how to configure this ‘look up’ task as part of the bridge configuration.

Before configuring data lookup, let us understand a little bit about the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] and the table from which the data is looked up. Assume that Humongous Insurance has a [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] subscription and have already created a database called **datalookupdb**. Also assume that within the database they have a table called **ClaimTypeLookup**. This table contains the mapping between **ClaimType** and **ClaimTypeDescription**. Here’s the script that can be run against the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] instance to create the **ClaimTypeLookup** table and populate it with the values.

```
USE datalookupdb 
GO 
CREATE TABLE ClaimTypeLookup 
( 
id int identity(1,1) primary key, 
ClaimType varchar(10), 
ClaimTypeDescription varchar(50) 
) 
GO 
INSERT INTO ClaimTypeLookup VALUES ('HI','Health Insurance') 
GO
```
This script (*AzureSQLDatabase_ClaimTypeLookup.sql*) is also available with the **FlatFile_Bridge** solution available for download from [http://go.microsoft.com/fwlink/?LinkID=249449](http://go.microsoft.com/fwlink/?LinkID=249449).

Note that the table is pre-populated with a record that maps a claim type, *HI*, to its description, *Health Insurance*. Essentially, this is how the table is used for lookup – the incoming flat-file message has the claim type information, for example, *HI*. However, the data that must be inserted into an on-premises SQL Server database must include the claim type description instead. So, at runtime, when the bridge is processing the message, it looks up ClaimTypeLookup table on [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)], sees that *HI* has the claim type description as *Health Insurance*, and uses the value *Health Insurance* in the message in addition to *HI*.

#### To configure data lookup from a SQL Database table

1. Within the pre-transform **Enrich** stage, select the **Enrich** activity, and then from the **Properties** pane click the ellipsis button **(…)** against the **Properties** property to open the **Property Definition** dialog box.

2. In the **Property Definitions** dialog box, click **Add** to open the **Add Property** dialog box. In the **Add Property** dialog box, do the following:

   |Section <br /> <br />|Field Name <br /> <br />|Description <br /> <br />|
   |-----------|--------------|---------------|
   |Source (Read From) <br /> <br />|Type <br /> <br />|For a lookup operation, select **Lookup** from the drop-down list. <br /> <br />|
   |Source (Read From) <br /> <br />|Identifier <br /> <br />|<ol><li>From the **Identifier** drop-down list, select **Configure New**. </li><li>In the **Provider Configuration** dialog box, specify the following values: <br /> <br />   Field Name <br /> <br />   Description <br /> <br />   **Provider Name** <br /> <br />   Specify a name for the provider. For this tutorial, specify **SqlDbLookupProvider**. <br /> <br />   **Connection String** <br /> <br />   Specify a valid connection string to connect to a [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table you created earlier. <br /> <br />   **Table Name** <br /> <br />   Specify the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table name from which you want to do a data lookup. For this tutorial, specify **ClaimTypeLookup**. <br /> <br />   **Query In Column** <br /> <br />   Specify a column name in the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table, the value of which is used as the input query for performing the data lookup. <br /> <br />   In this tutorial, you want to look up the claim description for a given claim type. So, specify this value as **ClaimType**. <br /> <br />   **Query Out Column** <br /> <br />   Specify a column name in the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table, the value of which is the output value that eventually gets assigned to the looked up property. <br /> <br />   In this tutorial, you want to retrieve the claim description for a given claim type. So, specify this value as **ClaimTypeDescription**. </li><li>Click **OK** to add the provider configuration. </li> </ol>|
   |Source (Read From) <br /> <br />|Lookup Property <br /> <br />|From the drop-down list, select a property that you must have already defined. The value of this property is passed on to the **Query In Column** specified in the provider configuration defined earlier. <br /> <br />For this tutorial scenario, the value for the **ClaimType** element in the incoming flat file message must be used to look up data in the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)]. So, in the drop-down select **ClaimType**. <br /> <br />|
   |Property (Write To) <br /> <br />|Property Name <br /> <br />|Specify a name for the property that contains the looked up value. The value of this property is derived from the value of the **Query Out Column** in the provider configuration defined earlier. <br /> <br />For this tutorial scenario, the value of **ClaimTypeDescription** property must be populated using the lookup. So, set this value to **ClaimTypeDescription**. <br /> <br />|
   |Property (Write To) <br /> <br />|Data Type <br /> <br />|Set the data type to **string**. <br /> <br />|
   Click **OK** in the **Add Property** dialog box and then in the **Property Definitions** dialog box. The dialog boxes resemble the following:

   ![](/Image/FFBridge-ConfigureLookup.gif)

   Save the bridge configuration.

   This is how the definitions in the dialog box would work while the bridge processes the message:

   - The [!INCLUDE[bridge](/Token/bridge_md.md)] looks up the value of **ClaimType** element in incoming flat file message and matches it with a **ClaimType** value in the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table, **ClaimTypeLookup**.

   - If a match is found, the [!INCLUDE[bridge](/Token/bridge_md.md)] picks up the corresponding value from the **ClaimTypeDescription** column in the **ClaimTypeLookup** table.

   - The picked up value is then assigned to the property (**ClaimTypeDescription**) that is created under the **Write To** section of the dialog box. And finally, the data type of the **ClaimTypeDescription** property is set to **string**.

3. Save changes to the project.

This procedure demonstrated how to configure a data lookup from a [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table by using which the value from the [!INCLUDE[ssSDS](/Token/ssSDS_md.md)] table becomes assigned to a **ClaimTypeDescription** variable. But, how do we assign this value from the **ClaimTypeDescription** property to the relevant element (ClaimTypeDescription) in the Insert message schema for writing the data into the on-premises [!INCLUDE[ssSDS](/Token/ssSDS_md.md)]? To do so, we use the **GetContextProperty**[!INCLUDE[mapop](/Token/mapop_md.md)] within a transform to pass the value from the context property to an element in the message. After the transform is created, you must include it as part of the bridge configuration. How to perform these tasks is described at [Step 7: Transform the Flat File Schema to the Insert Schema](/Topic/Step_7__Transform_the_Flat_File_Schema_to_the_Insert_Schema.md) describes how to create the transform, how to use the GetContextProperty [!INCLUDE[mapop](/Token/mapop_md.md)], and how to include the transform as part of [!INCLUDE[bridge](/Token/bridge_md.md)] configuration.

## See Also
[Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md)

