---
description: na
keywords: na
pagetitle: Get-AzureBizTalkBridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f468feb0-c000-4dbc-b591-df88e4823a9f
---
# Get-AzureBizTalkBridge
The **Get-AzureBizTalkBridge** lists [!INCLUDE[bridge](/Token/bridge_md.md)]s deployed to a [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. The cmdlet returns a collection of [!INCLUDE[bridge](/Token/bridge_md.md)]s based on the query.

## Syntax
`Get-AzureBizTalkBridge –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri <DeploymentUri> [-BridgePath <BridgePath>] [-Recurse] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL will result in an **ObjectNotFound** error. <br /> <br />|
|[-BridgePath *&lt;BridgePath&gt;*] <br /> <br />|Optional <br /> <br />|The path under which the list of bridges has to be retrieved. You can also specify the specified bridge to be retrieved. If you do not provide a path, the default value of “**\**” is assumed and all the bridges under the deployment endpoint are retrieved. <br /> <br />|
|[-Recurse] <br /> <br />|Optional <br /> <br />|If included, this parameter specifies that all the bridges under the sub-paths of the specified bridge path are retrieved as well. If this parameter is not included, only the bridges at the parent-level, immediately under the deployment endpoint are retrieved. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

