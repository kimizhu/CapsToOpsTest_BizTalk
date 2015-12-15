---
description: na
keywords: na
pagetitle: Creating .NET Applications Using TPM OM REST API
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1464cb6-685d-47ea-8596-bc4655234fc8
---
# Creating .NET Applications Using TPM OM REST API
Use the WCF Data Services to create .NET applications that consume the data services exposed by the TPM OM. The TPM OM API is based on the OData protocol. This topic provides instructions on how to create .NET applications to perform operations on the TPM OM entities, such as defining partners, creating agreements, and so on.

## Typical Code Flow for using the API
The following illustration captures a typical code flow for creating a .NET application to use the TPM OM REST API:

![](/Image/BTS_Svc_TPM_Codeflow.png)

## Set up Your Computer
To start creating .NET applications for consuming data services exposed by TPM OM API, install [!INCLUDE[vs2012](/Token/vs2012_md.md)] and [!INCLUDE[ssAstoria](/Token/ssAstoria_md.md)] 5.0:

- Install Visual Studio from [http://msdn.microsoft.com/library/dd831853](http://msdn.microsoft.com/library/dd831853).

- Install WCF Data Services from [http://www.microsoft.com/download/details.aspx?id=29306](http://www.microsoft.com/download/details.aspx?id=29306).

- If you used a self-signed certificate while provisioning [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], you must add that certificate to trusted certificate store on the computer where you use the TPM OM API. Otherwise, you get error - `The underlying connection was closed: Could not establish "trust relationship for the SSL/TLS secure channel`. You do not need to perform this step if you used a certificate from a trusted signing authority.

## <a name="BKMK_FirstSteps"></a>The First Steps
This section lists the overall set of instructions that you must follow to create a .NET application using the TPM OM REST API. The instructions in this section assume that you create a C# application.

#### To create a C# application

1. Create a [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] C# project.

2. In the project Solution Explorer, right-click **References**, and then select **Add Service Reference**.

3. In the Add Service Reference dialog box, do the following:

   1. For the address, enter the URL where the TPM OM service metadata is hosted and select **Go**. A typical URL for metadata looks like:

      ```
      bts_svc_tpm_metadata
      ```
      In this URL, `https://mybiztalkservice.biztalk.windows.net` is your deployment URL, `default` is the default namespace, and `$PartnerManagement` is the endpoint suffix to retrieve the metadata.

   2. In the **Namespace** text box, enter a namespace, such as **PartnerManagement**.

   3. Select **OK** to add the reference to the [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] project.

4. In the .cs file, add a reference to the service namespace. For example, if the namespace for your C# project is `BtsServices` and the namespace for the service reference is `PartnerManagement`, add the following reference to your .cs file:

   ```
   using BtsServices.PartnerManagement;
   ```
   You can now start creating the entities, set their properties, and create relationships between the entities.

   > [!IMPORTANT]
   > Whenever you commit changes to the service context, you must always use the **Batch** save option. You can either set this option once when you create the context by using the following:
   > 
   > `context.SaveChangesDefaultOptions = SaveChangesOptions.Batch;`
   > 
   > Or, you can use it every time you save changes to a context.
   > 
   > `context.SaveChanges(SaveChangesOptions.Batch);`

## In This Section

- [Example: Creating an X12 Agreement in BizTalk Services Using the TPM OM API](/Topic/Example__Creating_an_X12_Agreement_in_BizTalk_Services_Using_the_TPM_OM_API.md)

- [Example: Creating an AS2 Agreement in BizTalk Services Using the TPM OM API](/Topic/Example__Creating_an_AS2_Agreement_in_BizTalk_Services_Using_the_TPM_OM_API.md)

## See Also
[Trading Partner Management Object Model &#40;TPM OM&#41;: API Reference](/Topic/Trading_Partner_Management_Object_Model__TPM_OM):%20API%20Reference.md)

