---
description: na
keywords: na
pagetitle: Save-AzureBizTalkArtifact
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 837a7ec2-bf02-4925-bbb7-47e474e5b462
---
# Save-AzureBizTalkArtifact
The **Save-AzureBizTalkArtifact** saves already uploaded artifacts to another location in the artifact store deployed to a [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

## Syntax
`Save-AzureBizTalkArtifact –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri <DeploymentUri> -ArtifactPath <ArtifactPath> -SavePath <SavePath> [-Overwrite] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL will result in an **ObjectNotFound** error. <br /> <br />|
|-ArtifactPath *&lt;ArtifactPath&gt;* <br /> <br />|Required <br /> <br />|The complete relative path of the node from where the artifacts to be copied must be retrieved. <br /> <br />|
|-SavePath *&lt;SavePath&gt;* <br /> <br />|Required <br /> <br />|The absolute path where the artifact must be saved to. <br /> <br />|
|[-Overwrite] <br /> <br />|Optional <br /> <br />|A flag that indicates whether the existing artifact at the given save path must be replaced. <br /> <br />In case the file name provided for the **–SavePath** parameter already exists then a **ResouceExists** error is thrown. In such cases, the existing file can we overwritten by passing the **-Overwrite** parameter. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Get a list of deployed artifacts at the root node**

   `Save-AzureBizTalkArtifact –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/PO1.xsd -SavePath ./TestFolder/PO1.xsd`

   *Output*

   ```
   Successfully copied the following files 
   ./Test/Samples/PO1.xsd
   ```

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

