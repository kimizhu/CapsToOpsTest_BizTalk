---
description: na
keywords: na
pagetitle: Add-AzureBizTalkArtifactAssembly
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ae8cfdd-ba04-44c3-b8af-69304d03bacd
---
# Add-AzureBizTalkArtifactAssembly
The **Add-AzureBizTalkArtifactAssembly** adds an assembly to the artifact store for the service namespace you enter.

## Syntax
`Add-AzureBizTalkArtifactAssembly –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri  <DeploymentUri> -FilePath <FilePath> [-Overwrite] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL will result in an **ObjectNotFound** error. <br /> <br />|
|-FilePath *&lt;FilePath&gt;* <br /> <br />|Required <br /> <br />|The complete path to the artifact file to be uploaded. <br /> <br />|
|[-Overwrite] <br /> <br />|Optional <br /> <br />|A flag that specifies whether the existing artifacts in the artifact store must be overwritten. If an artifact already exists with the same name or at the same path, a **ResourceExists** error is thrown, unless the **Overwrite** parameter is passed. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Successfully add an assembly**

   `Add-AzureBizTalkArtifactAssembly –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -FilePath C:\MyLocation\CustomCode.dll`

   *Output*

   `Successfully added artifact ‘CustomCode.dll’ to Artifact Store at https://myDeploymentUri .biztalk.windows.net/$GlobalArtifacts/$Assembly/CustomCode.CustomCode, CustomCode, Version=1.0.0.0, Culture=neutral, PublicKeyToken=15dc99171c58f11b`

- **Error when trying to add an artifact that already exists**

   `Add-AzureBizTalkArtifactAssembly –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -FilePath C:\MyLocation\CustomCode.dll`

   *Output*

   `ERROR: The specified artifact ‘CustomCode.dll’ already exists either with the same name or the same path in the artifact store at https://myDeploymentUri.biztalk.windows.net/$GlobalArtifacts/$Assembly/CustomCode.CustomCode, CustomCode, Version=1.0.0.0, Culture=neutral, PublicKeyToken=15dc99171c58f11b`

- **Error when the provided artifact type is not supported**

   `Add-AzureBizTalkArtifactAssembly –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -FilePath C:\MyLocation\PO.trfm`

   *Output*

   `ERROR: Artifact of type .trfm is not supported by this cmdlet`

- **Successfully overwriting an existing artifact**

   `Add-AzureBizTalkArtifactAssembly –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -FilePath C:\MyLocation\CustomCode.dll -Overwrite`

   *Output*

   `Successfully added artifact ‘CustomCode.dll’ to Artifact Store at https://myDeploymentUri .biztalk.windows.net/$GlobalArtifacts/$Assembly/CustomCode.CustomCode, CustomCode, Version=1.0.0.0, Culture=neutral, PublicKeyToken=15dc99171c58f11b`

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

