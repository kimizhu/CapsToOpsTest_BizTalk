---
description: na
keywords: na
pagetitle: Create the Fourth Coffee application to receive orders and return invoice
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dd9385be-73a8-42e7-885d-6257e5421b6c
---
# Create the Fourth Coffee application to receive orders and return invoice
In this section, we set up the application that represents the Fourth Coffee restaurant. This application reads the X12 850 purchase order sent to the **tosupplier** Azure blob container, generates the X12 810 invoice in response, and then routes the invoice to the EDI X12 receive bridge that is deployed as part of the X12 agreement. For this tutorial we use a console application that performs these tasks.

> [!NOTE]
> Instead of providing instructions on how to create the application, this topic focuses on explaining the **SupplierApp** sample application that is available to download at [http://go.microsoft.com/fwlink/p/?LinkId=390150](http://go.microsoft.com/fwlink/p/?LinkId=390150).

## Prerequisites
Ensure that the following requirements are met on the computer where you use the supplier application to process customer orders.

- Install the [!INCLUDE[azure_1](/Token/azure_1_md.md)] .NET SDK. You can download the SDK from [http://go.microsoft.com/fwlink/p/?LinkId=378265](http://go.microsoft.com/fwlink/p/?LinkId=378265).

- Install the certificate that was used to provision [!INCLUDE[af_integration](/Token/af_integration_md.md)] using the [!INCLUDE[azureportal1](/Token/azureportal1_md.md)].

## Create a BlobHelper class
The **BlobHelper** class downloads the blob from the specified container, deletes it after reading, and returns the downloaded data.

```
using System.Linq;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.StorageClient;

public static class BlobHelper
{
    public static string DequeueData(string containerName, string connectionString)
    {
        //create a storage account
        var storageAccount = CloudStorageAccount.Parse(connectionString);

        //create a blog client
        var blobClient = storageAccount.CreateCloudBlobClient();

        //access the container using the blob client
        var blobContainer = new CloudBlobContainer(containerName, blobClient);

        //read the blobs in the container and return the result
        var blobItem = blobContainer.ListBlobs().FirstOrDefault();
        if (blobItem != null)
        {
            var blob = blobContainer.GetBlobReference(blobItem.Uri.ToString());
            var result = blob.DownloadText();
            blob.DeleteIfExists();
            return result;
        }
        return null;
    }
}
```

## Use an EDI invoice template
This application uses an X12 810 invoice template file to generate the invoice message. The template file, **Invoice810.edi** is added to the solution under the Data folder. The application replaces the values in this template to generate the actual 810 invoice that is sent to the customer. The contents of the template file resemble the following:

```
ISA*00*          *00*          *ZZ*FourthCoffee   *ZZ*Contoso        *121127*0941*U*00401*000000001*0*T*:~
GS*IN*FROM-SUPPLIER*RECEIVE-APP*121127*0941*1*T*00401~
ST*810*ST02~
NN1*OrderId*Item*Quantity*OrderstatusAcceptedOrRejected*Email~
SE*3*ST02~
GE*1*1~
IEA*1*000000001~
```
This template file is created in concurrence to the agreement we created in the step [Create a trading partner agreement](/Topic/Create_a_trading_partner_agreement.md). While creating the agreement in your environment, if you specified the values that were different from the ones suggested in the tutorial, you must update the template file accordingly. For example, in your agreement if you specified a different set of values for the hosted partner and guest partner qualifiers, you must provide the same values in the template file as well.

## Create an EdiHelper class
The **EdiHelper** class generates an X12 810 invoice message in response to the X12 850 purchaser order message downloaded from the blob. This uses the **Invoice810.edi** template file under the project’s Data folder to generate the X12 810 invoice.

```
using System;
using System.IO;
using System.Linq;
using System.Reflection;

public static class EdiHelper
{
    private static string invoiceTemplate;

    static EdiHelper()
    {
        var assembly = Assembly.GetExecutingAssembly();
        var resourceName = "SupplierApp.Data.Invoice810.edi";
        using (var stream = assembly.GetManifestResourceStream(resourceName))
        using (var reader = new StreamReader(stream))
        {
            invoiceTemplate = reader.ReadToEnd();
        }
    }

    public static string GenerateInvoice(string message, bool orderAccepted)
    {
        var segements = message.Split(new[] { Environment.NewLine, "*", "~" }, StringSplitOptions.RemoveEmptyEntries).ToList();
        int begSegmentIndex = -1;
        var begSegment = segements.FirstOrDefault(
        x =>
        {
            begSegmentIndex++;
            return string.Compare(x, "BEG", ignoreCase: true) == 0;
        });

        if (begSegment == null || segements.Count <= begSegmentIndex + 7 || string.Compare(segements[begSegmentIndex + 7], "SAC", ignoreCase: true) != 0)
        {
            throw new InvalidOperationException("Invalid message input");
        }

        return invoiceTemplate
            .Replace("OrderId", segements[begSegmentIndex + 6])
            .Replace("Item", segements[begSegmentIndex + 8])
            .Replace("Quantity", segements[begSegmentIndex + 9])
            .Replace("OrderstatusAcceptedOrRejected", orderAccepted ? "Accepted" : "Rejected")
            .Replace("Email", segements[begSegmentIndex + 2]);    }
}
```

## Create an AcsHelper class
The **AcsHelper** class creates the ACS authentication tokens required to securely send messages to the EDI receive bridge deployed under the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription on [!INCLUDE[azure_2](/Token/azure_2_md.md)].

```
using System;
using System.Collections.Specialized;
using System.Linq;
using System.Net;
using System.Text;

public static class AcsHelper
{
    public static string GetAcsToken(string acsAddress, string serviceIdentityUsername, string serviceIdentityPassword, string appliesToAddress)
    {
        using (WebClient client = new WebClient())
        {
            client.BaseAddress = acsAddress;

            var values = new NameValueCollection();
            values.Add("wrap_name", serviceIdentityUsername);
            values.Add("wrap_password", serviceIdentityPassword);
            values.Add("wrap_scope", appliesToAddress);

            var responseBytes = client.UploadValues("WRAPv0.9/", "POST", values);

            var response = Encoding.UTF8.GetString(responseBytes);

            // Extract the SWT token and return it.
            return response
                .Split('&')
                .Single(value => value.StartsWith("wrap_access_token=", StringComparison.OrdinalIgnoreCase))
                .Split('=')[1];
        }
    }
}
```

## Create a PipelineHelper class
The **PipelineHelper** class sends the X12 810 invoice message to the EDI X12 receive bridge that is deployed to your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

```
using System;
using System.IO;
using System.Net;
using System.Text;
using System.Web;

public static class PipelineHelper
{
    public static void SendToPipeline(string pipelineAddress, string acsAddress, string issuerName, string issuerKey, string message)
    {
        var appliesToUriBuilder = new UriBuilder(pipelineAddress);
        appliesToUriBuilder.Scheme = "http";
        if (appliesToUriBuilder.Port == 443)
        {
            appliesToUriBuilder.Port = -1;
        }

        var acstoken = AcsHelper.GetAcsToken(acsAddress, issuerName, issuerKey, appliesToUriBuilder.Uri.ToString());

        var webRequest = (HttpWebRequest)WebRequest.Create(pipelineAddress);
        webRequest.Method = "POST";
        webRequest.Headers[HttpRequestHeader.Authorization] = "WRAP access_token=\"" + HttpUtility.UrlDecode(acstoken) + "\"";

        var requestStream = webRequest.GetRequestStream();

        // convert string to stream
        var byteArray = Encoding.UTF8.GetBytes(message);
        var stream = new MemoryStream(byteArray);
        stream.CopyTo(requestStream);
        requestStream.Close();

        using (var response = webRequest.GetResponse()) ;
    }
}
```

## Create the Program.cs
The Program.cs invokes the other helper classes in the following order:

1. Calls the **DequeueData** method in the **BlobHelper** class and retrieves the message from the **toSupplier** blob.

2. Calls the **GenerateInvoiceMessage** method in the **EdiHelper** class to generate the X12 810 invoice in response.

3. Calls the **SendToPipeline** method in the **PipelineHelper** class to send the invoice message to the EDI receive bridge. The **PipelineHelper** class in turn uses the **AcsHelper** class to generate the authentication token required to securely send the message to the bridge.

The following code demonstrates this:

```
using System;
using System.Configuration;
using System.Net;
using System.Threading;

public class Program
{
    public static void Main(string[] args)
    {
        ServicePointManager.ServerCertificateValidationCallback += (data, server, chain, errors) => true;

        Console.WriteLine("Starting SupplierApp: {0}", ConfigurationManager.AppSettings["SupplierAppName"]);
        try
        {
            while (true)
            {
                Console.WriteLine("Being to get messages from blob");
                var message = BlobHelper.DequeueData(ConfigurationManager.AppSettings["BlobContainerName"], ConfigurationManager.AppSettings["BlobConnectionString"]);
                Console.WriteLine("Retrieved message from blob. MessageText: {0}", Environment.NewLine + message);
                if (message != null)
                {
                    Console.Write("Do you want to accept order (Y/N) : ");
                    var userInput = Console.ReadKey();
                    Console.WriteLine();

                    string invoiceBody;
                    if (userInput.Key == ConsoleKey.Y)
                    {
                        invoiceBody = EdiHelper.GenerateInvoice(message, orderAccepted: true);
                    }
                    else if (userInput.Key == ConsoleKey.N)
                    {
                        invoiceBody = EdiHelper.GenerateInvoice(message, orderAccepted: false);
                    }
                    else
                    {
                        throw new NotSupportedException("Invalid input");
                    }

                    Console.WriteLine("Begin to send message to pipeline");
                    PipelineHelper.SendToPipeline(
                        ConfigurationManager.AppSettings["PipelineAddress"],
                        ConfigurationManager.AppSettings["AcsAddress"],
                        ConfigurationManager.AppSettings["IssuerName"],
                        ConfigurationManager.AppSettings["IssuerKey"],
                        invoiceBody);

                    Console.WriteLine("Sent invoice to pipeline");
                }
                else
                {
                    Console.WriteLine("Messages not found in blob. Sleeping");
                    Thread.Sleep(TimeSpan.FromSeconds(1));
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("Exiting App. Unknown exception occurred. {0}", ex.ToString());
        }
    }
}
```

## Provide the configuration values and run the application
All the user-specific values used in this application are specified in the app.config file. You can provide the values as shown here:

```
<configuration>
  <appSettings>
    <add key="SupplierAppName" value="Fourth Coffee Application"/>
    <add key="BlobContainerName" value="tosupplier"/>
    <add key="BlobConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<mystorageaccount>;AccountKey=<connection_string>" />
    <add key="PipelineAddress" value="https://<mybiztalkservice>.biztalk.windows.net/default/Agreements/<id>/Receive" />
    <add key="AcsAddress"  value="https://<mybiztalkservice>.accesscontrol.windows.net/" />
    <add key="IssuerName" value="owner" />
    <add key="IssuerKey" value="<issuer_key>" />
  </appSettings>
</configuration
```
Save all changes to the project, and then build/run the application. The application will run infinitely polling the blob container (**tosupplier**) you specified in the application configuration.

## See Also
[Using BizTalk Services from a Windows 8 Application](/Topic/Using_BizTalk_Services_from_a_Windows_8_Application.md)

