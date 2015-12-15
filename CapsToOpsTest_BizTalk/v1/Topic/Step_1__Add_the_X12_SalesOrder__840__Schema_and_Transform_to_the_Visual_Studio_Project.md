---
description: na
keywords: na
pagetitle: Step 1: Add the X12 SalesOrder (840) Schema and Transform to the Visual Studio Project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f004ff0-232a-4835-a05f-147c627e4f06
---
# Step 1: Add the X12 SalesOrder (840) Schema and Transform to the Visual Studio Project
In this step, you include the X12 840 sales order schema in your project. You also create a [!INCLUDE[transform](/Token/transform_md.md)] to map the elements in the X12 schema and the **SalesOrder** schema you created in [Step 2: Create SalesOrder Schema](/Topic/Step_2__Create_SalesOrder_Schema.md). This is required because the EDI [!INCLUDE[bridge](/Token/bridge_md.md)] configured using the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] sends the message to the EAI bridge, which expects the incoming messages in the **SalesOrder** schema.

> [!NOTE]
> In this step, you add the X12 840 sales order schema and the [!INCLUDE[transform](/Token/transform_md.md)] to the **EAIEDITutorial**[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. However, you can always create a new project for just the schema and the [!INCLUDE[transform](/Token/transform_md.md)]. Typically, you should create a **BizTalk Service Artifacts** project for such schemas and [!INCLUDE[transform](/Token/transform_md.md)]s. For more information about this project type, see [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md).

### To include the X12 840 schema in the Visual Studio project

1. Download the EDI X12 schemas from [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057). The schema is available as part of the **MicrosoftEdiXSDTemplates.zip** package.

2. Right click the **EAIEDITutorial** project in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)], point to **Add**, and then click **Existing Item**. Navigate to the location where you downloaded and extracted the schemas, select the X12 840 schema (X12_00401_840.xsd), and add it to the project.

3. Create a [!INCLUDE[transform](/Token/transform_md.md)] between the X12 840 schema and the SalesOrder schema. You must create a [!INCLUDE[transform](/Token/transform_md.md)] to extract the values you want from the X12 message and reflect them in the **SalesOrder** message. Specify the name of the map as **EDI840ToSalesOrder.trfm**. For instructions, see [Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md).

### To include a transform

1. In [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)], right-click the **EAIEDITutorial** project, point to **Add**, and then click **New Item**.

   > [!NOTE]
   > If you want to use an already created map, you can use the **EDI840ToSalesOrder.trfm** map. This map is available as part of the sample available from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=316856).

2. In the **Add New Item** dialog box, select **Map**, specify the map name as **EDI840ToSalesOrder.trfm**, and then click **OK**.

3. In Solution Explorer, double-click the **EDI840ToSalesOrder.trfm** file to open the map.

4. In the [!INCLUDE[transform](/Token/transform_md.md)] window, select the source schema to **X12_00401_840.xsd** and the destination schema to **ECommerceSalesOrder.xsd**.

5. Directly map the following nodes in the source and destination schemas:

   |Source Schema <br /> <br />|Destination Schema <br /> <br />|
   |-----------------|----------------------|
   |N1Loop1/N2/N201 <br /> <br />|CompanyCode <br /> <br />|
   |PO1Loop1/PO1/PO107 <br /> <br />|PartID <br /> <br />|
   |PO1Loop1/PO1/PO102 <br /> <br />|Quantity <br /> <br />|
   |PO1Loop1/PO1/PO104 <br /> <br />|AskPrice <br /> <br />|
   |N1Loop1/N3/N301 <br /> <br />|Address/Line1 <br /> <br />|
   |N1Loop1/N3/N302 <br /> <br />|Address/Line2 <br /> <br />|
   |N1Loop1/N4/N401 <br /> <br />|Address/City <br /> <br />|
   |N1Loop1/N3/N402 <br /> <br />|Address/State <br /> <br />|
   |N1Loop1/N4/N404 <br /> <br />|Address/Country <br /> <br />|
   |N1Loop1/N4/N403 <br /> <br />|Address/Zipcode <br /> <br />|
   |PER/PER02 <br /> <br />|Contact/Firstname <br /> <br />|
   |PER/PER04 <br /> <br />|Contact/Lastname <br /> <br />|

6. Map the elements from the source schema (X12_00401_840) to the **RequestShipmentDate** element. The element in the source message that has the requested shipment date is **BQT05**. The value in that element is in the format YYYYMMDD. The value that must be entered in **SalesOrder** schema must be of the form YYYY-MM-DD. So, to achieve that, you must map the **BQT05** and **RequestShipmentDate** elements as shown in the screenshot below:

   ![](/Image/EAIEDI_RqShipDate.gif)

   To achieve this mapping, this is what you must do:

   1. Drag and drop a **String Extract**[!INCLUDE[mapop](/Token/mapop_md.md)] on the mapper surface and connect it to the BTS05 element from the source schema. Double-click the **String Extract**[!INCLUDE[mapop](/Token/mapop_md.md)] and set the **Start Index** property to **1** and the **End Index** property to **4**.

   2. Drag and drop a **String Extract**[!INCLUDE[mapop](/Token/mapop_md.md)] on the mapper surface and connect it to the BTS05 element from the source schema. Double-click the **String Extract**[!INCLUDE[mapop](/Token/mapop_md.md)] and set the **Start Index** property to **5** and the **End Index** property to **6**.

   3. Drag and drop a **String Extract**[!INCLUDE[mapop](/Token/mapop_md.md)] on the mapper surface and connect it to the BTS05 element from the source schema. Double-click the **String Extract**[!INCLUDE[mapop](/Token/mapop_md.md)] and set the **Start Index** property to **7** and the **End Index** property to **8**.

   With this, you have now extracted the values for YYYY, MM, and DD. You must now use the **String Concatenate**[!INCLUDE[mapop](/Token/mapop_md.md)] to join the extracted values using a hyphen (-). This is how the configuration for the **String Concatenate**[!INCLUDE[mapop](/Token/mapop_md.md)] looks like.

   ![](/Image/EAIEDI_RqShipDate_Concat.gif)

   In this screenshot, **Input_0**, **Input_2**, and **Input_4** are from the **String Extract**[!INCLUDE[mapop](/Token/mapop_md.md)]s that are connected to the **String Concatenate**[!INCLUDE[mapop](/Token/mapop_md.md)]. Values for **Input_1** and **Input_3** are set as hyphens (-). After this [!INCLUDE[mapop](/Token/mapop_md.md)], the value that will be transferred to the **RequestShipmentDate** element will be in the format YYYY-MM-DD.

   You must now connect the **String Concatenate**[!INCLUDE[mapop](/Token/mapop_md.md)] to the **RequestShipmentDate** element in the destination schema.

7. Repeat the tasks in the previous step to map the **BQT03** element in the source schema to the **DateNow** element in the destination schema. The mapped elements must look like the following:

   ![](/Image/EAIEDI_DateNow.gif)

8. To populate a value in the **Comments** element, map the N201 element in the source schema with the Comments element in the destination schema using the **String Concatenate**[!INCLUDE[mapop](/Token/mapop_md.md)].

   1. Drag and drop a **String Concatenate**[!INCLUDE[mapop](/Token/mapop_md.md)] on the mapper surface.

   2. Double-click the [!INCLUDE[mapop](/Token/mapop_md.md)] to open the **Configure String Concatenate** dialog box and set the Input_0 property to “**Order from partner** “. Click **OK**.

   3. Connect the **N201** element in the source schema to the **String Concatenate**[!INCLUDE[mapop](/Token/mapop_md.md)] and then join the **mapop** to the **Comments** element in the destination schema. The configuration for the [!INCLUDE[mapop](/Token/mapop_md.md)] must resemble the following:

      ![](/Image/EAIEDI_MapComments.gif)

      With this configuration, if the value in the **N201** element in the source schema is *XYZ*, for example, the value in the **Comments** element in the destination schema will be set to *Order from Partner XYZ*.

9. Save changes to the map.

## See Also
[Create and Deploy the Trading Partner Agreement](/Topic/Create_and_Deploy_the_Trading_Partner_Agreement.md)

