---
description: na
keywords: na
pagetitle: PowerShell Cmdlets for the BizTalk Adapter Service
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 711decf9-e1a5-4534-890f-00e6f0337d8b
---
# PowerShell Cmdlets for the BizTalk Adapter Service
Install and use the PowerShell cmdlets in [!INCLUDE[lobconnect](/Token/lobconnect_md.md)].

The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server utilizes the cmdlet (command-let) ability of PowerShell to expose the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] entities. Using PowerShell, Administrators can manage the Runtime Service and these LOB entities.

## Install the PowerShell cmdlets

1. Install Windows PowerShell 3.0.

2. Run the [!INCLUDE[af_integration](/Token/af_integration_md.md)] setup file. See [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md).

**Additional**

- The PowerShell cmdlets are automatically installed when the **Tools** option is selected during the setup. See [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md).

- When the installation completes, the **C:\Program Files\Windows Azure BizTalk Services Tools** folder is created. This folder contains the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime PowerShell module.

## Use the PowerShell cmdlets

1. Select Windows PowerShell and Run as Administrator.

   If User Account Control (UAC) is enabled, select Yes is prompted to proceed.

2. Type: **import-module "C:\Program Files\Windows Azure BizTalk Services Tools\Microsoft.BizTalk.Adapter.Services.Powershell.dll"**

3. Select Enter.

4. To view the cmdlets, type: **get-module**. **get-module** displays the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] and [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] cmdlets supported by the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] module.

**Additional**

- The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Windows PowerShell module name is Microsoft.BizTalk.Adapter.Services.Powershell.dll. PowerShell scripts written using the Preview-version of the cmdlets may fail after upgrading.

- When using **import-module**, modules exist only when the PowerShell command window is open; which is the current PowerShell session. When the PowerShell command window is closed, the session is closed and the module is removed.

## PowerShell Best Practices

|||
|-|-|
|**Case sensitivity** <br /> <br />|PowerShell commands are **not** case-sensitive. As a result, focus on the correct syntax and spelling. <br /> <br />|
|**Cmdlet Parameter Shortcuts** <br /> <br />|By default, PowerShell allows any unique prefix for the cmdlet parameters. For example, **-f**, **-fo** and **-for** can all be used as a shortcut for the -ForceDelete parameter. <br /> <br />|
|**Install Runtime &amp; Tools** <br /> <br />|Install on the same server. This option allows you to manage the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] components in the cloud and use the PowerShell cmdlets (command-lets) on a central server. <br /> <br />The Developer portion of the Setup should be installed on a separate computer. The goal is to separate the development tasks from the runtime tasks. <br /> <br />|
|**Service Bus Namespace** <br /> <br />|When using the –Namespace parameter, always enter the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace. <br /> <br />|
|**get-help &#42;cmdletName&#42; -full** <br /> <br />|Use -full to get detailed information on the cmdlet, including examples and a description of each parameter. <br /> <br />|
|**about_ topics** <br /> <br />|The PowerShell **about_** help topics are available in text format at C:\Windows\System32\WindowsPowerShell\v1.0\en-US. <br /> <br />|

## In This Section
[BizTalk Adapter Service PowerShell CmdLets - LobRelay](/Topic/BizTalk_Adapter_Service_PowerShell_CmdLets_-_LobRelay.md)

[BizTalk Adapter Service PowerShell CmdLets - LobTarget](/Topic/BizTalk_Adapter_Service_PowerShell_CmdLets_-_LobTarget.md)

[General PowerShell Cmdlets for BizTalk Adapter Service](/Topic/General_PowerShell_Cmdlets_for_BizTalk_Adapter_Service.md)

## See Also
[Windows PowerShell Cmdlet Help Topics](http://go.microsoft.com/fwlink/p/?LinkId=113277)
[LOB Security in BizTalk Adapter Service](/Topic/LOB_Security_in_BizTalk_Adapter_Service.md)
[Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md)

