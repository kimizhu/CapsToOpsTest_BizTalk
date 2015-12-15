---
description: na
keywords: na
pagetitle: PowerShell CmdLets to manage the BizTalk Service
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 381e888e-1289-4cc2-a2fa-58128379d72c
---
# PowerShell CmdLets to manage the BizTalk Service
This section lists the PowerShell cmdlets for management operations on [!INCLUDE[af_integration](/Token/af_integration_md.md)]. [!INCLUDE[af_integration](/Token/af_integration_md.md)] also provides PowerShell cmdlets for managing [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]. See [PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md).

## Install the PowerShell Cmdlets
To install the PowerShell cmdlets:

1. Install the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK. See [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md) for instructions.

2. Open the PowerShell window with administrator privileges.

3. Run **import-module** to import the [!INCLUDE[af_integration](/Token/af_integration_md.md)] module to the current session.

   ```
   import-module "C:\Program Files\Windows Azure BizTalk Services Tools\Microsoft.BizTalk.Services.Powershell.dll"
   ```
   > [!NOTE]
   > When using **import-module**, modules exist only when the PowerShell command window is open; which is the current PowerShell session. When the PowerShell command window is closed, the session is closed and the module is removed.

   > [!CAUTION]
   > If you used these PowerShell cmdlets in the Preview release of the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK to build PowerShell scripts, you must update those to include the right import path.

## Sample PowerShell Cmdlets
You can download [Azure BizTalk Service Management Sample](http://go.microsoft.com/fwlink/p/?LinkId=335967) that demonstrates how to use the PowerShell cmdlets. It also demonstrates use of some sample cmdlets that can be used for backing up and restoring [!INCLUDE[af_integration](/Token/af_integration_md.md)], retrieving [!INCLUDE[af_integration](/Token/af_integration_md.md)] properties, and syncing [!INCLUDE[ac2](/Token/ac2_md.md)] keys.

## In This Section

- [Get-AzureBizTalkBridge](/Topic/Get-AzureBizTalkBridge.md)

- [Remove-AzureBizTalkBridge](/Topic/Remove-AzureBizTalkBridge.md)

- [Add-AzureBizTalkArtifactXmlSchema](/Topic/Add-AzureBizTalkArtifactXmlSchema.md)

- [Add-AzureBizTalkArtifactTransform](/Topic/Add-AzureBizTalkArtifactTransform.md)

- [Add-AzureBizTalkArtifactAssembly](/Topic/Add-AzureBizTalkArtifactAssembly.md)

- [Add-AzureBizTalkArtifactCertificate](/Topic/Add-AzureBizTalkArtifactCertificate.md)

- [Get-AzureBizTalkArtifact](/Topic/Get-AzureBizTalkArtifact.md)

- [Save-AzureBizTalkArtifact](/Topic/Save-AzureBizTalkArtifact.md)

- [Remove-AzureBizTalkArtifact](/Topic/Remove-AzureBizTalkArtifact.md)

- [Start-AzureBizTalkBridgeSource](/Topic/Start-AzureBizTalkBridgeSource.md)

- [Stop-AzureBizTalkBridgeSource](/Topic/Stop-AzureBizTalkBridgeSource.md)

- [Get-AzureBizTalkBridgeSource](/Topic/Get-AzureBizTalkBridgeSource.md)

- [Restart-AzureBizTalkService](/Topic/Restart-AzureBizTalkService.md)

- [Clear-AzureBizTalkTrackingStore](/Topic/Clear-AzureBizTalkTrackingStore.md)

## See Also
[PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md)

