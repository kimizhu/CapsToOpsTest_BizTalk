---
description: na
keywords: na
pagetitle: Start-AzureBizTalkBridgeSource
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e87cfa5-c7e6-4956-bd06-c55838706da6
---
# Start-AzureBizTalkBridgeSource
You can have more than one source associated with a bridge configuration. The **Start-AzureBizTalkBridgeSource** starts one or all the sources deployed as part of a bridge configuration. If the &lt;SourceName&gt; parameter is passed, then that particular source is started. Otherwise, all the sources for the bridge are started.

## Syntax
`Start-AzureBizTalkBridgeSource –AcsNamespace <AcsNamespace> -IssuerName <IssuerName> -IssuerKey <IssuerKey> –DeploymentUri <DeploymentUri> -BridgePath <Path> [-SourceName <SourceName>] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-AcsNamespace *&lt;AcsNamespace&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
|-IssuerName *&lt;IssuerName&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer name. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-IssuerKey *&lt;IssuerKey&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[ac2](/Token/ac2_md.md)] issuer key. Specifying incorrect [!INCLUDE[ac2](/Token/ac2_md.md)] credentials results in an authentication error. <br /> <br />|
|-DeploymentUri *&lt;DeploymentUri&gt;* <br /> <br />|Required <br /> <br />|The deployment URI for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, `https://myDeploymentUri.biztalk.windows.net/default/`. Specifying an incorrect URL will result in an **ObjectNotFound** error. <br /> <br />|
|-BridgePath *&lt;Path&gt;* <br /> <br />|Required <br /> <br />|The name of the bridge that you want to start the sources for. <br /> <br />|
|[-SourceName *&lt;SourceName&gt;*] <br /> <br />|Optional <br /> <br />|The bridge source name that you want to start. <br /> <br /><ul><li>In case the specified source name does not exist, an error **ObjectNotFound** error message is returned. </li><li>In case source name is not provided, then all the sources for that bridge are started and a success message is returned. </li><li>In case a source name is not provided, and there are no sources listed for a particular bridge, then a message is returned stating that there are no sources for the bridge. </li> </ul>|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Successfully start a bridge source**

   `Start-AzureBizTalkBridgeSource  –AcsNamespace myACS -IssuerName owner –IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -BridgePath XmlOneWayBridge1 –SourceName mySource`

   *Output*

   `Source ‘mySource’ for bridge ‘https://myDeploymentUri.biztalk.windows.net/default/XmlOneWayBridge/’ has been started successfully.`

- **Error when the specified source does not exist**

   `Start-AzureBizTalkBridgeSource –AcsNamespace myACS -IssuerName owner –IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -BridgePath XmlOneWayBridge1 –SourceName nonExistantSource`

   *Output*

   `ERROR: Source ‘nonExistantSource’ doesn’t exist for bridge ‘https://myDeploymentUri.biztalk.windows.net/default/XmlOneWayBridge/’`

- **Successfully starting multiple sources for a bridge**

   `Start-AzureBizTalkBridgeSource –AcsNamespace myACS -IssuerName owner –IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -BridgePath XmlOneWayBridge1`

   *Output*

   `The following sources were started for bridge ‘https://myDeploymentUri.biztalk.windows.net/default/XmlOneWayBridge/’ <br />mySource1`mySource2mySource3

- **Behavior when no sources exist for the specified bridge**

   `Start-AzureBizTalkBridgeSource –AcsNamespace myACS -IssuerName owner –IssuerKey *<issuer key>* –DeploymentUri https://myDeploymentUri.biztalk.windows.net/default -BridgePath XmlOneWayBridge1`

   *Output*

   `No sources exist for bridge ‘https://myDeploymentUri.biztalk.windows.net/default/XmlOneWayBridge/’`

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

