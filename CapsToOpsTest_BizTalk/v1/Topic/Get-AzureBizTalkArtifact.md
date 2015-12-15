---
description: na
keywords: na
pagetitle: Get-AzureBizTalkArtifact
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1d2eeb2-270e-4b4b-b585-8e055402f01d
---
# Get-AzureBizTalkArtifact
The **Get-AzureBizTalkArtifact** lists the artifacts from the artifact store deployed to a [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. This cmdlet supports wildcards as well.

## Syntax
`Get-AzureBizTalkArtifact –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri <DeploymentUri> -[ArtifactPath <ArtifactPath>] [-Recurse] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL will result in an **ObjectNotFound** error. <br /> <br />|
|[-ArtifactPath *&lt;ArtifactPath&gt;*] <br /> <br />|Optional <br /> <br />|The relative path of the node from where the artifacts must be retrieved. If you do not provide a path, the default value of “**\**” is assumed and all the artifacts under the deployment endpoint are retrieved. <br /> <br />You can also provide wildcards to specify the type of artifact (&#42;.cer or &#42;.trfm) to be retrieved. <br /> <br />|
|[-Recurse] <br /> <br />|Optional <br /> <br />|If included, this parameter specifies that all the artifacts under the sub-paths of the deployment URI are retrieved as well. If this parameter is not included, only the artifacts at the parent-level, immediately under the deployment endpoint are retrieved. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Get a list of deployed artifacts at the root node**

   `Get-AzureBizTalkArtifact –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default`

   *Output*

   ```
   TestDll.dll
   TestCert.cer
   TestXsd.xsd
   TestTrfm.trfm
   ```

- **Get a list of all deployed schemas**

   `Get-AzureBizTalkArtifact –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples\*.xsd -Recurse`

   *Output*

   ```
   Samples/PO.xsd
   Samples/PO1.xsd
   Samples/GettingStarted/PO2.xsd
   ```

- **Retrieve a single artifact**

   `Get-AzureBizTalkArtifact –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/PO1.xsd`

   *Output*

   `Samples/PO1.xsd`

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

