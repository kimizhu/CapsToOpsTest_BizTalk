---
description: na
keywords: na
pagetitle: Step 2: Create SalesOrder Schema
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ff6545f-a395-48d9-80d9-c756f987bf98
---
# Step 2: Create SalesOrder Schema
Create a **SalesOrder** schema. Contoso sends sales order messages to Northwind using this schema. You can use the Schema Editor ([Tools for Creating Message Schemas](/Topic/Tools_for_Creating_Message_Schemas.md)) to build this schema or download the schema at [MSDN Code Gallery](http://go.microsoft.com/fwlink/p/?LinkId=316856).

### To create the SalesOrder schema

1. Right-click the project name (EAIEDITutorial), select **Add**, and then select **New Item**.

2. In **Add New Item**, select **Schema**, name it **ECommerceSalesOrder**, and then select **Add**.

3. Edit and build the schema to resemble the following:

   ```
   <xs:schema xmlns="http://ECommerceSalesOrder.Inbound" xmlns:b="http://schemas.microsoft.com/BizTalk/2003" 
   targetNamespace="http://ECommerceSalesOrder.Inbound" xmlns:xs="http://www.w3.org/2001/XMLSchema">
     <xs:element name="SalesOrder">
       <xs:complexType>
         <xs:sequence>
           <xs:element name="CompanyCode" type="xs:string" />
           <xs:element name="PartID" type="xs:int" />
           <xs:element name="Quantity" type="xs:int" />
           <xs:element name="AskPrice" type="xs:decimal" />
           <xs:element name="RequestShipmentDate" type="xs:date" />
           <xs:element name="Address">
             <xs:complexType>
               <xs:sequence>
                 <xs:element name="Line1" type="xs:string" />
                 <xs:element name="Line2" type="xs:string" />
                 <xs:element name="City" type="xs:string" />
                 <xs:element name="State" type="xs:string" />
                 <xs:element name="Country" type="xs:string" />
                 <xs:element name="Zipcode" type="xs:int" />
               </xs:sequence>
             </xs:complexType>
           </xs:element>
           <xs:element name="Contact">
             <xs:complexType>
               <xs:sequence>
                 <xs:element name="Firstname" type="xs:string" />
                 <xs:element name="Lastname" type="xs:string" />
               </xs:sequence>
             </xs:complexType>
           </xs:element>
           <xs:element name="Comments" type="xs:string" />
           <xs:element name="DateNow" type="xs:date" />
         </xs:sequence>
       </xs:complexType>
     </xs:element>
   </xs:schema>
   ```

4. Save the changes.

## See Also
[Create and Deploy the BizTalk Services Project](/Topic/Create_and_Deploy_the_BizTalk_Services_Project.md)

