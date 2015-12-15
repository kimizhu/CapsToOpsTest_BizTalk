---
description: na
keywords: na
pagetitle: Using BizTalk Services from a Windows 8 Application
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22a84afb-9a98-4eb5-b52f-919784f30e56
---
# Using BizTalk Services from a Windows 8 Application
[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], with its REST and .NET interfaces, can be used from a variety of applications, such as Windows 8 applications, to create an end-to-end integration solution. This tutorial demonstrates how trading partners can onboard themselves onto their partner’s [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment, and how end users can use modern Windows 8 applications to send messages to bridges deployed on [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For better understanding, this tutorial uses an end-to-end business scenario that showcases how different personas involved in a business process can be integrated using [!INCLUDE[af_integration](/Token/af_integration_md.md)].

## Business scenario
Contoso, Ltd. is a car manufacturing company looking to build a system, *Cloud Car*, that provides rich experience to their customers by enabling connectivity to cloud and the rich set of services that are available via the cloud. To start with, Contoso, Ltd. envisions a modern application that enables customers to search for available services in the surrounding areas on the go (gas stations, restaurants, etc.), browse through the service catalogs they offer (fuel prices, restaurant menus, etc.), and then order the service they wish to use. As a first step, Contoso, Ltd. plans to start this service with a restaurant, Fourth Coffee. Contoso, Ltd. intends to build an end-to-end system that is scalable to easily onboard more and more partners, while also providing rich end-user experience to the customers that will be using the service. At a high-level, Contoso, Ltd. wants to enable the following end-to-end application experience for its customers:

- A customer of Contoso, Ltd. launches the *Cloud Car* application from the car, and chooses to look at the nearby dining options.

- The *Cloud Car* application determines the car’s location and suggests the nearest location of Fourth Coffee, a dine-in/drive-in restaurant.

- After selecting the Fourth Coffee restaurant, the customer is presented with the menu available at the restaurant. The customer selects the items of interest and places the order.

- The Fourth Coffee Restaurant is notified of the customer’s order, processes it, and sends the invoice back to Contoso, Ltd., which in turn sends it to the customer via e-mail.

## <a name="BKMK_Scenario"></a>Implementing the business scenario
To implement the business scenario, Contoso, Ltd. decides to use Microsoft integration offerings, especially, [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. For the end-user application, one the customer can use from their cars, Contoso, Ltd. decides to use a [!INCLUDE[win8_client_2](/Token/win8_client_2_md.md)] modern app.

Before understanding the application flow, let us assume that one of the prerequisites for the application flow is already completed, which is Fourth Coffee must have already registered itself as a partner in the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal. Fourth Coffee uses the Trading Partner Management OM REST API to onboard itself as a partner. It also uses the REST API to register the menu options it provides for dining.

After this one-time task is completed, this is how the application flows:

1. A customer of Contoso, Ltd. uses the *Cloud Car* application, which is a [!INCLUDE[win8_client_2](/Token/win8_client_2_md.md)] modern app. Using the app, the customer selects the nearest location of the Fourth Coffee restaurant, looks at the menu, selects the items of choice, and places the order.

   The order request, which is in the form of an XML message, is sent to a [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)] (purchase order [!INCLUDE[bridge](/Token/bridge_md.md)]) that Contoso, Ltd. deploys as part of its [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

2. The bridge processes the message (validates the message against the expected message schema, transforms it to an X12 purchase order (850), etc.), and then routes it to an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob (purchase order blob). The bridge also inserts the purchase order message into an on-premise SQL Server database.

3. An [!INCLUDE[azure_2](/Token/azure_2_md.md)] worker role continually polls the [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob and reads the 850 purchase order message from the blob.

4. The worker role routes the purchase order from the blob to an EDI Send [!INCLUDE[bridge](/Token/bridge_md.md)], also deployed under Contoso, Ltd.’s [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

5. The EDI Send [!INCLUDE[bridge](/Token/bridge_md.md)] processes the purchase order and routes it to another [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob for the supplier, Fourth Coffee.

6. Using an application, the Fourth Coffee restaurant reads the message from the blob, accepts or rejects the order, and generates an X12 810 invoice.

7. The Fourth Coffee restaurant application sends the EDI X12 invoice back to the EDI receive bridge deployed by Contoso, Ltd.

8. The EDI receive bridge, processes the incoming X12 810 invoice, and then routes the message to another EAI bridge (invoice bridge) deployed by Contoso, Ltd. to process the invoice messages.

9. The EAI invoice bridge does the following:

   - Processes the message and routes it to an [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob storage.

   - Inserts the invoice data into an on-premises SQL Server database.

   - Sends an e-mail to the customer with the order details.

The following illustration depicts the end-to-end scenario.

![](/Image/WABS_CloudCar_AppFlow.png)

## Personas involved in the scenario
Contoso, Ltd. aims at delivering an end-to-end *Cloud Car* solution, which can be used by the partners (such as Fourth Coffee to easily onboard themselves and list their item catalogs) as well as end users to access the different services as they are on the move. To deliver this experience, Contoso, Ltd. must create four different, but connected applications.

- A self-service application to onboard partners, such as Fourth Coffee, that enables partners to register them with [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal for Contoso, Ltd., and enter the details for the services that they offer.

- An integration layer that accepts customer request messages, processes the purchase order and invoice messages, and sends communication out to the end users. This integration layer is created using [!INCLUDE[af_integration](/Token/af_integration_md.md)] and other [!INCLUDE[azure_2](/Token/azure_2_md.md)] technologies.

- An application for the Fourth Coffee restaurant to receive purchase order message, generates invoice, and send it back to the [!INCLUDE[azure_2](/Token/azure_2_md.md)] integration layer.

- And finally, a [!INCLUDE[win8_client_2](/Token/win8_client_2_md.md)] application that the customers can use to browse the service, place orders, etc.

To map the tutorial to these personas, this tutorial is divided into four parts, with each part focusing on a specific persona.

## Before you begin
Before you start with this tutorial, make sure you have provisioned [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. For instructions, see [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?linkid=302280).

## How to use this tutorial
This tutorial is written around samples which are available to download from the MSDN code gallery. You can either use the samples and go through this tutorial to understand how the sample was built or just use this tutorial to create your own end-to-end solution. Because this tutorial aims to showcase the capabilities of [!INCLUDE[af_integration](/Token/af_integration_md.md)], for components based on [!INCLUDE[af_integration](/Token/af_integration_md.md)], the tutorial provides steps on how to create those components in your environment. For other components used to set up the end-to-end solution, such as partner onboarding application, console application to process customer orders, and Windows 8 application to place orders, the tutorial uses the components provided with the sample and does not go into the details of how to create those applications from the start. Also, to be consistent with the sample, the names of artifacts (e.g. schemas, transforms, etc.) used in this tutorial are same as that in the sample.

The samples available from the MSDN code gallery contain different components, representing the different personas involved with the tutorial. The sample cannot include the configuration that you must do on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] on Azure. For that, you must follow the steps in this tutorial to set up your EDI agreement. This is how you should use the sample to set up the end-to-end solution.

1. Use the [PartnerOnboarding sample application](http://go.microsoft.com/fwlink/p/?LinkId=390146) from the sample package to onboard a partner. Make changes to the application as described in [Set up the application to onboard partners](/Topic/Set_up_the_application_to_onboard_partners.md) to use the application in your [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment.

2. The **CloudCar_Integration** component represents the integration layer for the sample. You could either follow the instructions in the tutorial at [Set up the integration layer](/Topic/Set_up_the_integration_layer.md) to create your own integration component, or use the one provided with the sample and make relevant changes to use it in your [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment. The changes required to use it in your environment are provided as part of the instructions at the [sample download location](http://go.microsoft.com/fwlink/p/?LinkId=390148).

   The integration layer also uses an [!INCLUDE[azure_2](/Token/azure_2_md.md)] worker role. You can use the code **BlobPollerRole** component, make changes to the configuration values, and deploy it under your [!INCLUDE[azure_2](/Token/azure_2_md.md)] subscription.

3. Use the [SupplierAppConsole sample application](http://go.microsoft.com/fwlink/p/?LinkId=390150) from the sample package to represent the Fourth Coffee application to approve or reject orders. Make configuration changes to the application, as described at [Create the Fourth Coffee application to receive orders and return invoice](/Topic/Create_the_Fourth_Coffee_application_to_receive_orders_and_return_invoice.md), to use it in your [!INCLUDE[azure_1](/Token/azure_1_md.md)] and [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment.

4. Use the [CloudCar Windows 8 sample application](http://go.microsoft.com/fwlink/p/?LinkId=390151) to look for Fourth Coffee restaurants, pull up their menu, and place an order. Make changes to the application, as described at [Create the Windows 8 customer application](/Topic/Create_the_Windows_8_customer_application.md), to use it in your environment, and then follow the instructions at [Test the solution](/Topic/Test_the_solution.md) to test the end-to-end solution flow.

> [!NOTE]
> Information about all the samples available as part of this tutorial is available in the [Download the samples](/Topic/Download_the_samples.md) topic.

## In This Section

- [Set up the application to onboard partners](/Topic/Set_up_the_application_to_onboard_partners.md)

- [Set up the integration layer](/Topic/Set_up_the_integration_layer.md)

- [Create the Fourth Coffee application to receive orders and return invoice](/Topic/Create_the_Fourth_Coffee_application_to_receive_orders_and_return_invoice.md)

- [Create the Windows 8 customer application](/Topic/Create_the_Windows_8_customer_application.md)

- [Test the solution](/Topic/Test_the_solution.md)

- [Download the samples](/Topic/Download_the_samples.md)

