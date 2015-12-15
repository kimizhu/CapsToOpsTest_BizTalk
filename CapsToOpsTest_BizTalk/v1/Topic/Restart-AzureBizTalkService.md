---
description: na
keywords: na
pagetitle: Restart-AzureBizTalkService
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dee3cad2-98dd-4e46-9a34-487a8f012fb1
---
# Restart-AzureBizTalkService
Use **Restart-AzureBizTalkService** to restart specific [!INCLUDE[af_integration](/Token/af_integration_md.md)].

## Syntax
`Restart-AzureBizTalkService –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri <DeploymentUri> [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL will result in an **ObjectNotFound** error. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Restart a [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription**

   `Restart-AzureBizTalkService –AcsNamespace myACS -IssuerName owner –IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default`

   *Output*

   `BizTalk Service - ‘https://myDeploymentUri.biztalk.windows.net/default’ restarted successfully`

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

