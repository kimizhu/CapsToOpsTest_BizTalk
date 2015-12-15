---
description: na
keywords: na
pagetitle: General PowerShell Cmdlets for BizTalk Adapter Service
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9899d19-f752-45d8-9fa1-815fa7f6b2e2
---
# General PowerShell Cmdlets for BizTalk Adapter Service
The **Get-BizTalkService** cmdlet returns the [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL associated with the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime.

## Syntax
`Get-BizTalkService [-ServerUrl <String>] [-SkipCertCheck] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-ServerUrl *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime server URL is the URL of local Management Service, which is: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br /><ul><li>If a valid server URL is specified, the associated [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL is returned. </li><li>If an invalid or no server URL is specified, an error is returned. </li> </ul>|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Use this parameter if you want to skip the certificate check. <br /> <br />|
|*CommonParameters* <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples
Here are some examples:

- **Successfully get the [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL associated with the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime**

   `Get-BizTalkService -ServerUrl http://localhost:8080/BAService/ManagementService.svc`

   *Output*

   `https://myDeploymentUrl.biztalk.windows.net/default`

- **Error when specified [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime URL does not exist**

   `Get-BizTalkService -ServerUrl http://MyServer:8080/BAService/ManagementService.svc`

   *Output*

   `ERROR: Unable to connect to the service using the specified server URL`

## See Also
[PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md)

