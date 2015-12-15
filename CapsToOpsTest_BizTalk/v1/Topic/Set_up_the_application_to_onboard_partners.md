---
description: na
keywords: na
pagetitle: Set up the application to onboard partners
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a868bed2-401c-4d35-84fd-1fc7cce23ab4
---
# Set up the application to onboard partners
This topic provides information on an ASP.NET application that uses the Trading Partner Management OM API to enable partners, such as Fourth Coffee restaurant, to onboard themselves as trading partners in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] under the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription of Contoso, Ltd. The ASP.NET application uses the [Trading Partner Management Object Model &#40;TPM OM&#41;: API Reference](/Topic/Trading_Partner_Management_Object_Model__TPM_OM):%20API%20Reference.md) API to create partners, create business profiles for the partner, and add custom data for the partner such as dining menu items, their description and prices, etc.

This topic does not go into the detail of creating the application. Instead, you can download the **PartnerOnboarding** application from the MSDN code gallery at [http://go.microsoft.com/fwlink/p/?LinkId=390146](http://go.microsoft.com/fwlink/p/?LinkId=390146).

## Prerequisites
Ensure that the following requirements are met on the computer where you use the partner onboarding application.

- Install Visual Studio from [http://msdn.microsoft.com/library/dd831853](http://msdn.microsoft.com/library/dd831853).

- Install WCF Data Services from [http://www.microsoft.com/download/details.aspx?id=29306](http://www.microsoft.com/download/details.aspx?id=29306).

- Get the REST endpoint for the TPM OM API. This is required to discover the TPM OM entities like partners, business profiles, etc. and then perform actions like creating a partner, creating a business profile, etc.

   Typically, if the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription name for Contoso, Ltd. is **mybiztalkservice** (as an example), the REST endpoint for discovering the TPM OM entities will be `https://*mybiztalkservice*.biztalk.windows.net/default/$PartnerManagement`.

- Install the certificate that was used to provision [!INCLUDE[af_integration](/Token/af_integration_md.md)] using the [!INCLUDE[azureportal1](/Token/azureportal1_md.md)].

## How to use the PartnerOnboarding application
To understand how to create an application that uses the TPM OM API, see [Creating .NET Applications Using TPM OM REST API](/Topic/Creating_.NET_Applications_Using_TPM_OM_REST_API.md). The first step is to generate a context to the WCF Data Services-based REST endpoint by adding a service reference to the endpoint `https://**mybiztalkservice**.biztalk.windows.net/default/$PartnerManagement`, where *mybiztalkservice* is the name of your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. Once you have done that, you can use the generated context to access the TPM OM entities such a **Partner**, **BusinessProfile**, etc. To get a list of all the TPM OM entities, see [TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md).

The **PartnerOnboarding** sample already includes the generated TPM context. However, you must provide the endpoint for Contoso’s [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription, and other associated details, to create partners in Contoso’s [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment. You must also provide the correct ACS endpoint address, issuer name, and issuer key. This is required to perform secure operations against the [!INCLUDE[af_integration](/Token/af_integration_md.md)] endpoint.

You can provide these values for the **baseUri**, **acsAddress**, **issuerName**, and **issuerKey** variables in the **PartnerController.cs** class of the **PartnerOnboarding** sample.

> [!NOTE]
> The **PartnerOnboarding** application provides the capabilities to onboard different kinds of service providers as partners, such as partners offering fuel services, tire services, etc. However, for the purpose this tutorial, we only look at the food category. So, even though the code to onboard partners of other categories is available in the sample, it is commented out. You can un-comment the code snippets in **Index.cshtml** and **SupplierCatalog.cs** to light up the capabilities to onboard other service partners as well.

## Run the application
After you have made the required changes to the application code, build and run the application to add a partner for Contoso, Ltd. Once the web page launches, provide the following details:

1. For **Name**, enter **FourthCoffee** and provide a description.

2. Select **Food** as the category.

3. Provide a URL for the logo image for your restaurant. You must add a logo because this will be used to point the location of the supplier on the map.

4. Select **Fetch your coordinates** to determine your exact position. These coordinates are also included as custom data while adding the partner in Contoso, Ltd.’s [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment.

5. Select **Add Item** and add the menu items (item name, item description, item price, and a photo of the food item) that Fourth Coffee offers. The photo you upload will be visible to the customers from their Windows 8 application, while they place the order.

6. Select **Submit**.

   ![](/Image/WABS_CloudCar_CreatePartner.PNG)

Once the partner is successfully added, a message is displayed on the web page.

## See Also
[Using BizTalk Services from a Windows 8 Application](/Topic/Using_BizTalk_Services_from_a_Windows_8_Application.md)

