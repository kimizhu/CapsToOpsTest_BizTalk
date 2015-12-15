---
description: na
keywords: na
pagetitle: Test the solution
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df136217-8b16-463e-a4d5-4aadc4018d7d
---
# Test the solution
In this topic, we test the end-to-end solution by using all the applications and components that we have set up so far. Before testing the solution, make sure you have set up all the components as required.

1. Make sure you have completed the instructions in the step [Set up the application to onboard partners](/Topic/Set_up_the_application_to_onboard_partners.md) to create a partner called **FourthCoffee**. You must have also provided a logo for FourthCoffee and added a menu item to the catalog to choose from.

   > [!NOTE]
   > For the purposes of this demo, the solution works best when only one menu item is added as part of the catalog.

2. Ensure you have set up the integration layer with all the required components:

   1. Make sure you have created and deployed the **PurchaseOrderBridge**[!INCLUDE[one-way](/Token/one-way_md.md)] in [!INCLUDE[af_integration](/Token/af_integration_md.md)], as described in the step [Create a BizTalk Service project to process purchase orders](/Topic/Create_a_BizTalk_Service_project_to_process_purchase_orders.md).

   2. Make sure you have created and deployed the **InvoiceBridge**[!INCLUDE[one-way](/Token/one-way_md.md)] in [!INCLUDE[af_integration](/Token/af_integration_md.md)], as described in the step [Create a BizTalk Service project to process invoices](/Topic/Create_a_BizTalk_Service_project_to_process_invoices.md).

   3. Make sure you have created an agreement to process messages exchanged between Contoso, Ltd. and Fourth Coffee, as described in the step [Create a trading partner agreement](/Topic/Create_a_trading_partner_agreement.md).

   4. Make sure you have created, deployed, and started a [!INCLUDE[azure_1](/Token/azure_1_md.md)] worker role that polls an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob container and routes purchase order messages to send bridge in the EDI agreement, as described in the step [Create an Azure worker role to poll the Azure blob](/Topic/Create_an_Azure_worker_role_to_poll_the_Azure_blob.md).

3. Make sure you have created and started the application that is used by Fourth Coffee to accept or reject orders, as described in the step [Create the Fourth Coffee application to receive orders and return invoice](/Topic/Create_the_Fourth_Coffee_application_to_receive_orders_and_return_invoice.md).

4. While creating a trading partner agreement you must have provided a relay endpoint where suspended messages that fail processing are routed to. Make sure you have an application listening to that relay endpoint. For this purpose, you can use the sample tool, [Azure BizTalk Services EAI Sample Tools - Message Receiver](http://go.microsoft.com/fwlink/p/?LinkId=389581) provided with [!INCLUDE[af_integration](/Token/af_integration_md.md)].

5. On a Windows 8 computer, start the **CloudCar** application. From the Visual Studio Solution Explorer, right-click the solution name and select **Build**. Once the build is complete, run the simulator to test the application:

   1. In the Simulator, tap the **Contoso CloudCar** icon from the Start screen to launch the application.

   2. Once the application starts, tap the **Restaurant** icon.

      ![](/Image/WABS_CloudCar_Restaurant.png)

   3. When prompted whether the application can use your current location, select **Allow**.

   4. A map page launches and zooms into your current location. The map page shows the location of a nearby Fourth Coffee restaurant. The map uses the same logo icon to point the location of Fourth Coffee that you provided while creating a partner in the [Set up the application to onboard partners](/Topic/Set_up_the_application_to_onboard_partners.md).

      ![](/Image/WABS_CloudCar_Map.png)

   5. Tap the logo icon on the map to see the menu for the Fourth Coffee restaurant.

      ![](/Image/WABS_CloudCar_Order.png)

      Select an item from the menu to see the price and description. Provide the required details and tap **Submit Order** to place the order. If the order is successfully submitted, a message is displayed on the screen.

6. Switch to the computer where you are running the Fourth Coffee application to approve or reject orders. Because that application is represented using a console application in this tutorial, you must see a new X12 purchase order message on the console. Carefully study the contents of the purchase order. It must contain an order ID, customer name, customer e-mail address, order details, etc.

   ![](/Image/WABS_CloudCar_FourthCoffee.png)

   In the console application, at the prompt to accept or reject orders, enter “**y**” to accept the order

7. Switch to the computer where you have SQL Server installed and connect to the **CloudCarDatabase**. Run a SELECT query on the **Orders** table.

   ![](/Image/WABS_CloudCar_OrdersTable.png)

8. Similarly, run a SELECT query on the **Invoice** table in the **CloudCarDatabase**.

   ![](/Image/WABS_CloudCar_InvoiceTable.png)

9. Finally, you must have received an e-mail with the order details at the e-mail address you specified while placing the order. The contents of the e-mail resemble the following:

   ```
   Your order number is: 2792e39a-a170-4cfb-9d9c-e09d53e0fefc
   You ordered for: Chicken Salad
   Quantity ordered is: 1
   Your order has been: Accepted
   Thank You!
   ```

With this, you have tested an end-to-end solution where a partner on boards itself on another partner’s [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment, the hosting partner sets up an integration layer using [!INCLUDE[af_integration](/Token/af_integration_md.md)] and other [!INCLUDE[winazure](/Token/winazure_md.md)] technologies, and the customers use a mobile modern Windows 8 application to use the services.

