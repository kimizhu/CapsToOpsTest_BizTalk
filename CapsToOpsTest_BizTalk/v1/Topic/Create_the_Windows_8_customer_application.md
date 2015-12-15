---
description: na
keywords: na
pagetitle: Create the Windows 8 customer application
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a883230d-b3d9-472d-a4c9-56615bec12ff
---
# Create the Windows 8 customer application
In this section, we set up a Windows 8 application that can be used by customers from within a car to look for service partners associated with Contoso, Ltd., select the services they want to avail, and then order those services. Instead of providing instructions on how to create the application, this topic focuses on explaining the **CloudCar** application that is available as a sample download at [http://go.microsoft.com/fwlink/?LinkId=390151](http://go.microsoft.com/fwlink/?LinkId=390151).

## Prerequisites
Make sure you meet the following prerequisites on a computer running Windows 8.

- Install Windows SDK for Windows 8. For more information, see [http://msdn.microsoft.com/windows/desktop/hh852363.aspx](http://msdn.microsoft.com/windows/desktop/hh852363.aspx)

- Install WCF Data Services Tool for Windows Store Apps. You can download and install this tool from [http://go.microsoft.com/fwlink/?LinkId=389566](http://go.microsoft.com/fwlink/?LinkId=389566).

- Install Bing Maps Extension for Visual Studio. You can download and install the extension from [http://go.microsoft.com/fwlink/?LinkId=389565](http://go.microsoft.com/fwlink/?LinkId=389565).

- Familiarize yourself on how to use Bing maps in a Windows Store app. You can get the information to get started with Bing maps at [http://msdn.microsoft.com/library/hh846481.aspx](http://msdn.microsoft.com/library/hh846481.aspx)

- Generate a Bing maps key. For more information, see [http://go.microsoft.com/fwlink/?LinkId=389567](http://go.microsoft.com/fwlink/?LinkId=389567).

- Install the certificate that was used to provision [!INCLUDE[af_integration](/Token/af_integration_md.md)] using the [!INCLUDE[azureportal1](/Token/azureportal1_md.md)].

## Understanding the CloudCar Windows 8 application
Download and open the CloudCar Windows 8 application from [http://go.microsoft.com/fwlink/?LinkId=324220](http://go.microsoft.com/fwlink/?LinkId=324220). It contains two projects – **CloudCar** and **CloudCarServiceManager**.

- **CloudCar** is a Windows 8 application, which in turn contains the following:

   - **GroupedItemsPage.xaml** – This page lists the service categories that are available around the customer location. Because this tutorial only deals with restaurants, the page only has one category (food) to choose from. Other categories can be included as required from the SampleDataSource.cs file under the \DataModel folder in the solution.

      Once customers select a category from this page, Bing map is loaded.

   - **MapPage.xaml** – This page renders the Bing map as part of the customer application, zooms to the customer location, and then points the location of the Fourth Coffee restaurant on the map.

      Once customers tap on the icon of Fourth Coffee restaurant on the map, a menu page is loaded.

   - **SplitPageFood.xaml** – This page lists the menu items that the customers can select from. The page also asks customers to provide details like their name, address, e-mail etc. These inputs are sent to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] bridge in the form of an XML message.

      Once the customers have provided all the details, they can also submit their order from this page.

- **CloudCarServiceManager** is used to perform the background tasks like sending messages to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] bridge, etc. This project contains the following components:

   - **CustomerOrder.cs** – This is used to construct the XML message from the details (name, e-mail, address, contact number) provided by the customer.

   - **SupplierCatalog.cs** – This is used to retrieve and load the supplier catalog on the **SplitPageFood.xaml** page in the Windows 8 application.

   - **MessageSender.cs** – This is used to send the customer order to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] bridge deployed on [!INCLUDE[azure_2](/Token/azure_2_md.md)].

   - **CloudCarServiceManager.cs** – This uses all the other classes to perform the entire task. This class first authenticates with the [!INCLUDE[af_integration](/Token/af_integration_md.md)] using ACS tokens. After that, it sets up a data context and uses the **SupplierCatalog** class to retrieve the catalog offered by the partner. After that, it uses the **CustomerOrder** to create an XML message and then uses **MessageSender** to send the XML message to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] bridge.

> [!IMPORTANT]
> The **CloudCar** Windows 8 application has the capability to locate other service providers as well such as re-fueling, tire services, etc. However, for this tutorial demo we only look at the food service category. You can un-comment relevant code snippets in the file **SampleDataSource.cs** (under the **DataModel** folder), to look up other service providers as well. To use services provided by other service providers, you must have already added them as partners in those specific categories using the **PartnerOnboarding** application.

## Use the CloudCar application
You must make the following changes to use the CloudCar Windows 8 application to work with your [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment.

1. In the file **MapPage.xaml**, replace the placeholder INSERT_YOUR_BING_MAPS_KEY with your Bing Maps Key.

   ```
   <bm:Map Credentials="INSERT_YOUR_BING_MAPS_KEY" x:Name="myMap" Grid.Row="1" Grid.ColumnSpan="2" RenderTransformOrigin="0.496,0.49"></bm:Map>
   ```

2. In the file **CloudCarServiceManager.cs**, provide the following values:

   - For the variable, **tpmBaseUri**, specify the base URI relevant to your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription to retrieve the metadata for the TPM context.

   - For the variable **acsAddress**, specify the ACS address used for your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

   - For the variable **issuerName**, specify the owner for the ACS namespace.

   - For the variable **issuerKey**, specify the shared secret key for the ACS namespace.

   - In the following snippet, replace the placeholder [BIZTALK_SERVICE_SUBSCRIPTION_NAME] with your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription name.

      ```
      await MessageSender.SendMessage("https://[BIZTALK_SERVICE_SUBSCRIPTION_NAME].biztalk.windows.net/default/PurchaseOrderBridge", purchaseOrder, "application/xml");
      ```

3. In the file **MessageSender.cs**, replace the placeholder with your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription name.

   ```
   private static string baseUri = "https://[BIZTALK_SERIVCE_SUBSCRIPTION_NAME].biztalk.windows.net/default/PurchaseOrderBridge";
   ```

4. Build and run the application.

## See Also
[Using BizTalk Services from a Windows 8 Application](/Topic/Using_BizTalk_Services_from_a_Windows_8_Application.md)

