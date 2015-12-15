---
description: na
keywords: na
pagetitle: Step 4: Create a Transform to Map the SalesOrder Schema to the Insert Operation Schema
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 655b7e77-7681-4fe4-92ec-7795d24aba97
---
# Step 4: Create a Transform to Map the SalesOrder Schema to the Insert Operation Schema
Uses a [!INCLUDE[transform](/Token/transform_md.md)] to map the SalesOrder schema (ECommerceSalesOrder.xsd) to the schema of the Insert operation on the SalesOrder table.

### To configure a transform

1. In [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], right-click the **EAIEDITutorial** project, select **Add**, and then select **New Item**.

2. In **Add New Item**, select **Map**, enter **SalesOrder_SQL.trfm** for the map name, and then select **OK**.

3. In Solution Explorer, double-click the **SalesOrder_SQL.trfm** file to open the map.

4. In the [!INCLUDE[transform](/Token/transform_md.md)] window, set the source schema to **ECommerceSalesOrder.xsd** and the destination schema to **EAIEDITutorial_SalesOrder_TableOperation.dbo.SalesOrder.xsd**.

5. Directly map the following nodes in the source and destination schemas:

   |Source Schema <br /> <br />|Destination Schema <br /> <br />|
   |-----------------|----------------------|
   |CompanyCode <br /> <br />|CompanyCode <br /> <br />|
   |PartId <br /> <br />|PartNum <br /> <br />|
   |Quantity <br /> <br />|Qty <br /> <br />|
   |AskPrice <br /> <br />|UnitAskPrice <br /> <br />|
   |RequestShipmentDate <br /> <br />|ShipDate <br /> <br />|
   |Comments <br /> <br />|CustomerComments <br /> <br />|
   |DateNow <br /> <br />|DateRequested <br /> <br />|

6. Map the following nodes in the source and destination schemas using a **String Concatenate** map operation:

   |Source Schema <br /> <br />|Destination Schema <br /> <br />|
   |-----------------|----------------------|
   |Address\Line1 <br /> <br />|SellToAddress <br /> <br />BillToAddress <br /> <br />|
   |Address\Line2 <br /> <br />|SellToAddress <br /> <br />BillToAddress <br /> <br />|
   |Address\City <br /> <br />|SellToAddress <br /> <br />BillToAddress <br /> <br />|
   |Address\State <br /> <br />|SellToAddress <br /> <br />BillToAddress <br /> <br />|
   |Address\Country <br /> <br />|SellToAddress <br /> <br />BillToAddress <br /> <br />|
   |Address\ZipCode <br /> <br />|SellToAddress <br /> <br />BillToAddress <br /> <br />|
   |Contact\FirstName <br /> <br />|PartnerContact <br /> <br />|
   |Contact\LastName <br /> <br />|PartnerContact <br /> <br />|
   To map elements using the **String Concatenate** map operation, drag-and-drop the map operation from toolbox to the mapper area. Add each element from the source tree as an input to the map operation, and then connect the String Concatenate component to the elements in the destination schema. The follow illustration shows the transform with all the relevant elements mapped:

   ![](/Image/EAIEDITut_SO_SQL_Trfm.gif)

   > [!NOTE]
   > The SalesOrder_SQL.trfm is also available as part of the sample at [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=316856).

7. Save your changes to the map.

## See Also
[Create and Deploy the BizTalk Services Project](/Topic/Create_and_Deploy_the_BizTalk_Services_Project.md)

