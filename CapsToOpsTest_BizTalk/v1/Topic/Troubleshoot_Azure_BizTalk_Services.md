---
description: na
keywords: na
pagetitle: Troubleshoot Azure BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 89c29e95-c2fa-4a45-ace2-f2e31f59dc49
---
# Troubleshoot Azure BizTalk Services
When troubleshooting [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], you can use Tracking in the [!INCLUDE[tpm_full](/Token/tpm_full_md.md)] and use the Debug logs stored in the Storage account. This topic provides information on using the Tracking and Debug logs.

## Tracking
Every time the message sending client gets a response (whether it’s a failure or a success), the response header includes a tracking ID. In cases where there is a failure, you can extract this tracking ID from the header and use the [Tracking Messages in BizTalk Services portal](/Topic/Tracking_Messages_in_BizTalk_Services_portal.md) feature in [!INCLUDE[tpm_full](/Token/tpm_full_md.md)] to troubleshoot. The following code snippet demonstrates how to extract the tracking ID from the response:

```
byte[] requestBytes; // message transferred to bytes.

Try
{
  WebClient webClient = new WebClient();                 
  UriBuilder builder = new UriBuilder(this.bridgeRuntimeAddress) { Scheme = Uri.UriSchemeHttps };

  // one can also use GetWebResponse instead of UploadData.
  byte[] responseBytes = webClient.UploadData(builder.Uri, "POST", requestBytes);
}

Catch (WebException we)
{
  Console.Writeline("Received WebException while sending message. Details: ");
  HttpWebResponse httpWebExceptionResponse = we.Response as HttpWebResponse;
  if (httpWebExceptionResponse == null)
  {
    Console.Writeline("WebException contains no Http exception response. Status = {0}", we.Status);
  }
  else
  {
    if (!String.IsNullOrEmpty(httpWebExceptionResponse.Headers["TrackingId"]))
    {
      Console.Writeline ("TrackingId={0}", httpWebExceptionResponse.Headers["TrackingId"]);
    }
    else
    {
      Console.Writeline ("Did not find TrackingId header on the WebException");
    }
    Console.Writeline ("StatusCode = {0} and StatusDescription = {1}", httpWebExceptionResponse.StatusCode, 
      httpWebExceptionResponse.StatusDescription);
  }
}
```

## Debug Logs
During the development process, debug logs are available in the WADLogsTable in the Storage Account. To view these log files, you can use the following tools:

- [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/releases/view/89713)

- [Browsing Storage Resources with Server Explorer](http://msdn.microsoft.com/library/windowsazure/ff683677.aspx)

The debug log files include the following events:

- Loading an assembly

- Adding or updating an artifact, like a Transform

- Adding, updating, or deleting Bridge Configuration

- Message submitted to the Bridge pipeline

- Bridge stages including their Begin Execute and End Execute events

- Faults

## Windows Azure BizTalk Services tool in Visual Studio
The Windows Azure BizTalk Services tool is available as an Extension in Visual Studio. Using this tool, you can debug your bridge by sending a test message. The tool steps through the different stages of your bridge and shows the status after each stage. The tool also displays the individual tracking events with any errors. To add this tool:

1. In the Visual Studio project, go to the **Tools** menu, and select **Extensions and Updates**.

2. Select **Online**.

3. In Search, type **BizTalk**.

4. Select **BizTalk Service Explorer** from the list and download/install.

In Server Explorer, **Windows Azure BizTalk Services** is listed. You may have to close/reopen Visual Studio for it to display.

## See Also
[BizTalk Services](/Topic/BizTalk_Services.md)
[Troubleshoot the BizTalk Adapter Service](/Topic/Troubleshoot_the_BizTalk_Adapter_Service.md)

