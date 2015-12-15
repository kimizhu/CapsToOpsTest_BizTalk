---
description: na
keywords: na
pagetitle: Remove-AzureBizTalkBridge
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85e9ff1b-3792-4c54-ab21-f511dc82bc67
---
# Remove-AzureBizTalkBridge
The **Remove-AzureBizTalkBridge** deletes a [!INCLUDE[bridge](/Token/bridge_md.md)] deployed at a specific [!INCLUDE[af_integration](/Token/af_integration_md.md)] endpoint. If you have a bridge deployed at the relative address /A/B/C, and you perform a delete operation on /A, you get an error. Similarly, if you perform the delete operation at a relative address that does not exist, you get an error. You must perform the delete operation only at the complete relative address of an existing bridge.

## Syntax
`Remove-AzureBizTalkBridge –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri <DeploymentUri> -BridgePath <BridgePath> [-NoPrompt] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL results in an **ObjectNotFound** error. <br /> <br />|
|-BridgePath *&lt;BridgePath&gt;* <br /> <br />|Required <br /> <br />|The complete relative path to the bridge that needs to be deleted. If you provide a path that has one or more bridges deployed under it, you get an **InvalidOperation** error. Also, if you provide a path where no bridge is deployed, you get an **ObjectNotFound** error. <br /> <br />|
|[-NoPrompt] <br /> <br />|Optional <br /> <br />|If included, you are not prompted for a confirmation before the bridge is deleted. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Successfully delete a bridge**

   `Remove-AzureBizTalkBridge –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -BridgePath myBridge`

   *Output*

   `Successfully deleted bridge https://myDeploymentUri.biztalk.windows.net/default/myBridge`

- **Error when bridge is not found**

   `Remove-AzureBizTalkBridge –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -BridgePath myIncorrectBridge`

   *Output*

   `ERROR: Bridge not found. Could not find bridge https://myDeploymentUri.biztalk.Windows.net/default/myIncorrectBridge`

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

