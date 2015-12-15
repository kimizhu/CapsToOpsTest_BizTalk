---
description: na
keywords: na
pagetitle: Add-AzureBizTalkArtifactTransform
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3eb1bb5-f68d-4021-a932-0e7ee54de798
---
# Add-AzureBizTalkArtifactTransform
The **Add-AzureBizTalkArtifactTransform** adds a transform to the artifact store for the service namespace you enter.

## Syntax
`Add-AzureBizTalkArtifactTransform –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri  <DeploymentUri> -ArtifactPath <ArtifactPath> -FilePath <FilePath> [-Overwrite] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL will result in an **ObjectNotFound** error. <br /> <br />|
|-ArtifactPath *&lt;ArtifactPath&gt;* <br /> <br />|Required <br /> <br />|The complete artifact path in the artifact store. <br /> <br />|
|-FilePath *&lt;FilePath&gt;* <br /> <br />|Required <br /> <br />|The complete path to the artifact file to be uploaded. <br /> <br />|
|[-Overwrite] <br /> <br />|Optional <br /> <br />|A flag that specifies whether the existing artifacts in the artifact store must be overwritten. If an artifact already exists with the same name or at the same path, a **ResourceExists** error is thrown, unless the **Overwrite** parameter is passed. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Successfully add a transform artifact**

   `Add-AzureBizTalkArtifactTransform –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/GettingStarted/map.trfm -FilePath C:\MyLocation\map.trfm`

   *Output*

   `Successfully added artifact ‘map.trfm’ to Artifact Store at https://myDeploymentUri.biztalk.windows.net/$Artifacts/TransformDefinition/Samples/GettingStarted/map.trfm`

- **Error when trying to add an artifact that already exists**

   `Add-AzureBizTalkArtifactTransform –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/GettingStarted/map.trfm -FilePath C:\MyLocation\map.trfm`

   *Output*

   `ERROR: The specified artifact ‘map.trfm’ already exists either with the same name or the same path in the artifact store at https://myDeploymentUri.biztalk.windows.net/$Artifacts/TransformDefinition/Samples/GettingStarted/map.trfm`

- **Error when the provided artifact type is not supported**

   `Add-AzureBizTalkArtifactTransform –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/GettingStarted/PO.xsd -FilePath C:\MyLocation\PO.xsd`

   *Output*

   `ERROR: Artifact of type .xsd is not supported by this cmdlet`

- **Successfully overwriting an existing artifact**

   `Add-AzureBizTalkArtifactTransform –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/GettingStarted/map.trfm -FilePath C:\MyLocation\map.trfm -Overwrite`

   *Output*

   `Successfully added artifact ‘map.trfm’ to Artifact Store at https://myDeploymentUri.biztalk.windows.net/$Artifacts/TransformDefinition/Samples/GettingStarted/map.trfm`

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

