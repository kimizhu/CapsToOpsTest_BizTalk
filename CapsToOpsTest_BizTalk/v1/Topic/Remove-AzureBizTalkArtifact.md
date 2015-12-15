---
description: na
keywords: na
pagetitle: Remove-AzureBizTalkArtifact
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2f46aa-f407-4368-8362-3d0c9b5c1b48
---
# Remove-AzureBizTalkArtifact
The **Remove-AzureBizTalkArtifact** deletes artifacts from the artifact store deployed to a [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. Depending on the relative address at which you perform the delete operation, you get different responses:

- If you perform a delete operation against any occupied node, it deletes only that specific artifact.

- If you perform a delete operation against any unoccupied node or a non-existing artifact, the operation is ignored and returns success. This does not return an HTTP 404 error.

- If you perform a delete operation against the root node, it results in an error.

## Syntax
`Remove-AzureBizTalkArtifact –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri <DeploymentUri> -ArtifactPath <ArtifactPath> [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL will result in an **ObjectNotFound** error. <br /> <br />|
|-ArtifactPath *&lt;ArtifactPath&gt;* <br /> <br />|Required <br /> <br />|The complete relative path of the artifact node that must be deleted. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Successfully delete an artifact**

   `Remove-AzureBizTalkArtifact –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/PO1.xsd`

   *Output*

   `The Artifact ‘https://myDeploymentUri.biztalk.windows.net/$Artifacts/XmlSchemaDefinition/Samples/PO1.xsd’ was successfully removed.`

- **Error when the artifact to be deleted does not exist**

   `Remove-AzureBizTalkArtifact –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/PO2.xsd`

   *Output*

   `The Artifact ‘https://myDeploymentUri.biztalk.windows.net/$Artifacts/XmlSchemaDefinition/Samples/PO2.xsd’ doesn’t exist.`

- **Error when root node is provided instead of a specific artifact**

   `Remove-AzureBizTalkArtifact –AcsNamespace myACS -IssuerName owner -IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -ArtifactPath Samples/`

   *Output*

   `ERROR: Please provide specific artifact to be removed and not the root node`

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

