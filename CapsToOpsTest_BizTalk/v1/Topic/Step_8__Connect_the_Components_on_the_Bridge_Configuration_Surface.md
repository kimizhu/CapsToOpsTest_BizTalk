---
description: na
keywords: na
pagetitle: Step 8: Connect the Components on the Bridge Configuration Surface
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 881ddc2f-f224-4409-a027-cd227bb85fcc
---
# Step 8: Connect the Components on the Bridge Configuration Surface
The previous steps in this tutorial demonstrated how to add an FTP source, an LOB component, and a one-way bridge to [!INCLUDE[msgflow](/Token/msgflow_md.md)] surface. This step demonstrates how to connect all these components to create an end-to-end message flow.

### To connect the components on the bridge design surface

1. Open the MessageFlowItinerary.bcs file in the **FlatFile_Bridge** project.

2. From the **Toolbox**, select **Connection**, and drag-drop the mouse pointer from the FTP Source component to the bridge component to connect the two. Repeat this step to connect the bridge component to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] component.

3. Set the filter condition on the connection between the bridge and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] entity.

   1. Click the connection between [!INCLUDE[one-way](/Token/one-way_md.md)] and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] entity.

   2. In the **Properties** window, click the ellipsis **(…)** button for **Filter Condition**.

   3. In the **Route Filter Configuration** dialog box, set the filter condition to **Match All**. This ensures that all the messages that are processed through the bridge are routed to the LOB entity.

   4. Click **OK**.

4. Set the Route action so that the outgoing message to the LOB application has the appropriate SOAP action header.

   1. Open **Server Explorer** and navigate to the SQL [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] created earlier. Right click the relay, click **Properties**, and for the **Operations** property, copy the value of the first operation. This value denotes the value of the SOAP action header that must be set on the message that is routed to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)].

   2. On the [!INCLUDE[msgflow](/Token/msgflow_md.md)] surface, click the connection between [!INCLUDE[one-way](/Token/one-way_md.md)] and the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] entity.

   3. In the **Properties** window, click the ellipsis **(…)** button for **Route Action**. In the **Route Actions** dialog box, click **Add** to open the **Add Route Action** dialog box. In the **Add Route Action** dialog box, do the following:

   4. Under **Property (Read From)** section, select **Expression**, and then paste the value that you copied earlier.

      > [!IMPORTANT]
      > You must always specify the value for an expression within single quotes.

   5. Under **Destination (Write To)** section, set the Type to **SOAP** and the **Identifier** to **Action**.

      The dialog box resembles the following:

      ![](/Image/FFBridge-RouteAction.gif)

   6. Click **OK** in the **Add Route Action** dialog box to add the route action. Click **OK** in the **Route Actions** dialog box and then click **Save** to save changes to an [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

      The end-to-end message flow resembles the following:

      ![](/Image/FFBridge-MessageFlow.gif)

   7. Save changes to the project.

## See Also
[Tutorial: Using BizTalk Service Bridges to Lookup Data from Azure SQL Database](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Lookup_Data_from_Azure_SQL_Database.md)

