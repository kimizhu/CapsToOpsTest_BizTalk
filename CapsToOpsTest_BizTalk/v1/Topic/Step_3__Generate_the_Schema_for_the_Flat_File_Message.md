---
description: na
keywords: na
pagetitle: Step 3: Generate the Schema for the Flat File Message
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 89cc2a0d-ce11-4c15-9bde-08272986f1a3
---
# Step 3: Generate the Schema for the Flat File Message
As described in the business scenario, Northwind Traders sends a flat file message to Humongous Insurance. For Humongous Insurance, to process the message by using a one-way [!INCLUDE[bridge](/Token/bridge_md.md)], it must have the schema of the flat file message as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] created in the last step. [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides a **Flat File Schema Wizard** that generates a flat-file schema from an existing flat-file instance message. Humongous Insurance uses the flat-file message instance message that it received from Northwind Traders (out of band, over e-mail) and then uses the **Flat File Schema Wizard** to create the schema.

Assume that the flat file message (**SampleInsuranceClaim.txt**) that is sent to Humongous Insurance, looks like the following:

```
101|HI|1000.0|John;RedmondWay;Seattle;Washington|1234567
```
This topic demonstrates how to use the Flat File Schema wizard to generate a flat file schema by using **SampleInsuranceClaim.txt** as the input instance message. The sample file is also provided with the solution (**FlatFile_Bridge_Integration**) available as a download from [http://go.microsoft.com/fwlink/?LinkID=249449](http://go.microsoft.com/fwlink/?LinkID=249449).

### To use the Flat File Schema wizard

1. Right-click the **FlatFile_Bridge** project, point to **Add**, and then click **New Item**.

2. In the **Add New Item** dialog box, select **Generate Flat File Schema**, enter a name for the schema as **InsuranceClaim.xsd**, and then click **Add**. The Flat File Schema Wizard starts.

3. On the **Flat File Schema Information** screen, select your instance and enter the following information. When you are done, click **Next** to continue.

   1. **Instance file:** Click the **Browse** button to locate the flat file from which the schema will be generated. Browse to the folder that contains the text file you created in the Prerequisites section.

   2. **Record name:** Type **SourceClaim**. The value you specify here is the schema root name.

   3. **Target namespace:** Accept the default, **http://FlatFile_Bridge.InsuranceClaim** for schema target namespace.

4. On the **Select Document Data** screen, the contents of the flat file are displayed. Select the data needed for creating the schema, and then click **Next**. In this walkthrough, because we are using the entire document instance, you can press **Ctrl-A** to select all.

5. In the **Select Record Format** screen, you specify whether the records are formatted using a delimiter symbol or by defining relative positions. In the instance message we chose, the records are delimited using a pipe symbol (|), hence select **By delimiter symbol**, and then click **Next**.

6. On the **Delimited Record** screen, enter the following to define the first level of the schema and when you are done, click **Next**.

   1. **Child delimiter:** Select **|**.

   2. **Escape character:** An escape character is a single character that suppresses any special meaning of the character that follows it. See [Escape Characters](http://go.microsoft.com/fwlink/?LinkId=245838) for more information. For this walkthrough, leave this blank.

      > [!NOTE]
      > When using **\**, **{,** and **}** for **Child delimiter** or **Escape character**, a back slash must be used. For example, **\\,** and **\{**.

      ![](/Image/FFBridge-DelimitedRecord.gif)

   3. Click **Next** to continue.

7. The wizard identifies five elements in the **SourceClaim** record. Enter values for the elements as illustrated in the following table to define the elements under **SourceClaim** record:

   |Element Name <br /> <br />|Element Type <br /> <br />|Data Type <br /> <br />|
   |----------------|----------------|-------------|
   |Enter **ClaimID** <br /> <br />|Select **Field Element**. <br /> <br />|Select **positiveInteger** <br /> <br />|
   |Enter **ClaimType** <br /> <br />|Select **FieldElement** <br /> <br />|Select **string** <br /> <br />|
   |Enter **ClaimAmount** <br /> <br />|Select **FieldElement** <br /> <br />|Select **double** <br /> <br />|
   |Enter **PersonInfo** <br /> <br />|Select **Record** <br /> <br />||
   |Enter **PolicyId** <br /> <br />|Select **FieldElement** <br /> <br />|Select **string** <br /> <br />|
   ![](/Image/FFBridge-ChileElementsFirst.gif)

   Click **Next** to continue.

   > [!NOTE]
   > After you click **Next** on the **Child Elements** screen, you will not be able to click **Back** to redefine or make any changes to the child elements. For any changes, restart the wizard to define the flat file schema.

8. After you complete the steps until here, the first level of the schema is generated as shown in the **Schema View** page.

   ![](/Image/FFBridge-SchemaViewFirst.gif)

   Because we defined **PersonInfo** as a **Record** type, the Flat File Schema Wizard now continues to further define the **PersonInfo** record. On the **Schema View** page, select **PersonInfo**, and then click **Next** to continue.

9. On the **Select Document Data** page, select the segment that corresponds to the **PersonInfo** record,  as shown in the image below, and then click **Next** to define its child elements.

   ![](/Image/FFBridge-SelectDocDataFirst.gif)

10. On the **Select Record Format** page, select **By delimiter symbol**, and then click **Next**. Choose this option because the elements within the **PersonInfo** record are delimited using a symbol, semicolon (**;**).

11. On the **Delimited Record** page, enter the following to define the **PersonalInfo** record. When you are done, click **Next**.

   1. Select **;** from **Child delimiter** drop-down selection list.

   2. Leave the **Escape character** text box blank.

   ![](/Image/FFBridge-DelimitedRecordSecond.gif)

12. Using the values from the **Delimited Record** page, the wizard identifies four child elements. Provide values for the record elements as suggested in the following table.

   |Element Name <br /> <br />|Element Type <br /> <br />|Data Type <br /> <br />|
   |----------------|----------------|-------------|
   |Enter **Name** <br /> <br />|Select **Field Element**. <br /> <br />|Select **string** <br /> <br />|
   |Enter **Address** <br /> <br />|Select **FieldElement** <br /> <br />|Select **string** <br /> <br />|
   |Enter **City** <br /> <br />|Select **FieldElement** <br /> <br />|Select **string** <br /> <br />|
   |Enter **State** <br /> <br />|Select **FieldElement** <br /> <br />|Select **string** <br /> <br />|
   ![](/Image/FFBridge-ChildElementsSecond.gif)

13. You have defined all the nodes for the **SourceClaim** schema. On the **Schema View** page, click **Finish**.

   After you click **Finish**, the schema file you created, **InsuranceClaim.xsd**, is opened within the Visual Studio solution. You can now verify the schema that you created.

## See Also
[Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md)

