---
description: na
keywords: na
pagetitle: Create an Azure worker role to poll the Azure blob
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3b16ab7-7f26-4a29-9d86-87c95fa0f8d4
---
# Create an Azure worker role to poll the Azure blob
In the previous steps we created an [!INCLUDE[af_integration](/Token/af_integration_md.md)] bridge that receives the purchase order message from the customer, maps it to an X12 850, then routes it to a **purchaseorder** blob container. We also created an X12 agreement using the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to receive an X12 850 purchase order message, the message is then sent to the Fourth Coffee restaurant. In this step, we use an [!INCLUDE[azure_2](/Token/azure_2_md.md)] worker role that polls the **purchaseorder** blob container. It then sends the X12 850 purchase order blob to the X12 send bridge that is deployed as part of the X12 agreement.

This topic does not go into the details of creating an [!INCLUDE[winzaure2](/Token/winzaure2_md.md)] worker role. You can download the **BlobPollerRole** worker role sample from [http://go.microsoft.com/fwlink/p/?LinkId=390152](http://go.microsoft.com/fwlink/p/?LinkId=390152). You must make the following changes to the role configuration to use it in your environment.

## Prerequisites
Make sure you have the [!INCLUDE[azure_2](/Token/azure_2_md.md)] SDK for .NET is installed on the computer where you are using the worker role. You can download the SDK from [http://go.microsoft.com/fwlink/p/?LinkId=378265](http://go.microsoft.com/fwlink/p/?LinkId=378265).

## Update the worker role configuration
Make the following changes to use the **BlobPollerRole** worker role in your [!INCLUDE[azure_2](/Token/azure_2_md.md)] subscription.

1. Open the **BlobPollerRole** solution and in the Solution Explorer, expand **BlobPollerRole**, expand **Roles**, and then double-click **BlobPollerWorkerRole** to open the properties for this role.

2. On the Settings tab, make the following changes to the configuration properties.

   |||
   |-|-|
   |ACSAddress <br /> <br />|Provide the ACS URL associated with your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. <br /> <br />|
   |IssuerName <br /> <br />|Provide the issuer name for the ACS namespace. <br /> <br />|
   |IssuerKey <br /> <br />|Provide the issuer key for the ACS namespace. <br /> <br />|
   |PipelineAdderss <br /> <br />|Enter the pipeline endpoint where the blob poller must direct the message after reading from the blob. For this tutorial, this must be the endpoint where the EDI X12 send agreement is deployed. You can get the endpoint from Send Settings tab (Inbound URL view) of the X12 agreement you deployed earlier. The endpoint is typically in the format `https://*mybiztalkservice*.biztalk.windows.net/default/Agreements/*<id>*/Send`. <br /> <br />|
   |ContainerName <br /> <br />|Enter the blob container where the X12 850 purchase order messages are dropped. For this tutorial, enter this value as **purchaseorder**. You created this container in the earlier steps. <br /> <br />|
   |CloudStorageAccountConectionString <br /> <br />|Select the ellipsis (**…**) against the property and in the dialog box, enter the storage account name and the account access key. Select the option to use HTTPS connections, and then select **OK**. <br /> <br />|
   |ContentTypeValue <br /> <br />|For content type, enter **application/xml**. <br /> <br />|
   Save changes to the project.

3. Right-click the solution name in the Solution Explorer, and then select **Build**.

4. After the build completes successfully, right-click the **BlobPollerRole** in the Solution Explorer, then select **Package**. In the dialog box that appears, for **Service configuration**, select **Cloud**; and for **Build configuration**, select **Release**.

   Once the operation successfully completes, you will see that two files are created in the \BlobPoller\bin\Release\app-publish directory. In the next step, you upload these files to your [!INCLUDE[azure_2](/Token/azure_2_md.md)] subscription to deploy the worker role.

## Deploy the worker role on Azure

1. Open the [!INCLUDE[azure_2](/Token/azure_2_md.md)] Management Portal, and from the command bar, point to **New**, **Compute**, **Cloud Service**, and then select **Quick Create**.

2. Enter a URL for the worker role, select a region where the role will be deployed, and then select the checkmark.

3. Select the cloud service you created, select the Instances tab, make sure the **Production** view is selected, and then select **Upload** from the command bar.

4. In the **Upload a Package** dialog box, do the following:

   1. Provide a deployment label.

   2. For **Package**, browse to the \BlobPoller\bin\Release\app.publish location, and select the service package file (.cspkg).

   3. For **Configuration**, browse to the \BlobPoller\bin\Release\app.publish location, and select the cloud service configuration file (.cscfg).

   4. Select the checkbox to deploy the worker role even if it contains a single instance.

   5. Select the checkbox if you want to start the worker role after it is uploaded.

   6. Select the checkmark. Once the worker role is deployed, it will start polling the blob you specified in the configuration, until you stop the role from the [!INCLUDE[portal](/Token/portal_md.md)].

## See Also
[Set up the integration layer](/Topic/Set_up_the_integration_layer.md)

