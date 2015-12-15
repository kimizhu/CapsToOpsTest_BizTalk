---
description: na
keywords: na
pagetitle: Get-AzureBizTalkBridgeSource
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e5067d3-a411-4f38-a00c-ab199f90a5a9
---
# Get-AzureBizTalkBridgeSource
You can have more than one sources associated with a bridge configuration. The **Get-AzureBizTalkBridgeSource** cmdlet gets the status of a specified source or all the sources deployed for the specified bridge.

- If the status is returned as **True**, it denotes that the bridge source is started.

- If the status is returned as **False**, it denotes that the bridge source is stopped.

## Syntax
`Get-AzureBizTalkBridgeSource –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri <DeploymentUri> -BridgePath <BridgePath> [-SourceName <SourceName>] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL results in an **ObjectNotFound** error. <br /> <br />|
|-BridgePath *&lt;Path&gt;* <br /> <br />|Required <br /> <br />|The name of the bridge that you want to get the sources status for. <br /> <br />|
|[-SourceName *&lt;SourceName&gt;*] <br /> <br />|Optional <br /> <br />|The bridge source name that you want the status for. <br /> <br /><ul><li>In case the specified source name does not exist, an error **ObjectNotFound** error message is returned. </li><li>In case source name is not provided, then the status for all the sources is returned. </li><li>In case a source name is not provided, and there are no sources listed for a particular bridge, then a message is returned stating that there are no sources for the bridge. </li> </ul>|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Successfully retrieve the status of a bridge source**

   `Get-AzureBizTalkBridgeSource –AcsNamespace myACS -IssuerName owner –IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -BridgePath XmlOneWayBridge1 –SourceName mySource`

   *Output*

   `Bridge - ‘https://myDeploymentUri.biztalk.windows.net/default/XmlOneWayBridge1/`

   ```
   Source – mySource
   Status - True
   ```

- **Successfully retrieve status of all sources for a bridge**

   `Get-AzureBizTalkBridgeSource –AcsNamespace myACS -IssuerName owner –IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -BridgePath XmlOneWayBridge1`

   *Output*

   `The status of sources for bridge ‘https://myDeploymentUri.biztalk.windows.net/default.servicebus.Windows.net/XmlOneWayBridge/’`

   ```
   Source - mySource1
   Status - False
   ----------
   Source – mySource2
   Status - False                                                                                                               
   ----------
   Source – mySource3
   Status - True
   ```

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

