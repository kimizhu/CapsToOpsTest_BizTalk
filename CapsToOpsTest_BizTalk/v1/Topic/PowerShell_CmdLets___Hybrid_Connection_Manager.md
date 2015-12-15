---
description: na
keywords: na
pagetitle: PowerShell CmdLets | Hybrid Connection Manager
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0f1b5e9-dfd5-47c5-8023-539df683c05b
---
# PowerShell CmdLets | Hybrid Connection Manager
This topic lists the PowerShell cmdlets for the on-premises Hybrid Connection Manager.

When using Hybrid Connections for Azure applications, you install the Hybrid Connection Manager on the on-premises resource. The on-premises Hybrid Connection Manager includes Windows PowerShell cmdlets to manage the Hybrid Connections on your local computer, including:

- Add-HybridConnection

- Update-HybridConnection

- Remove-HybridConnection

- Get-HybridConnection

- Set-HybridConnectionManagerConfiguration

> [!NOTE]
> These cmdlets manage the on-premises listener connections to the Hybrid Connections. They do not add, update, or remove the Hybrid Connections in the [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployment on [!INCLUDE[azure_2](/Token/azure_2_md.md)].

To use the PowerShell cmdlets:

- You must be a member of the local Administrators group on the on-premises resource.

- You must run the cmdlets on the on-premises computer that has the Hybrid Connection Manager installed.

- From Programs, select **Windows PowerShell** and Run as Administrator. If User Account Control (UAC) is enabled, you may be prompted to proceed. Click **Yes**.

> [!IMPORTANT]
> The -ConnectionString parameter refers to the complete On-premises Connection String listed in the [!INCLUDE[azportal](/Token/azportal_md.md)]. [Create and Manage Hybrid Connections](http://azure.microsoft.com/documentation/articles/integration-hybrid-connection-create-manage/) lists the steps to copy the On-premises Connection String.

|Powershell Cmdlet <br /> <br />|Description <br /> <br />|Parameters <br /> <br />|
|---------------------|---------------|--------------|
|Add-HybridConnection <br /> <br />|Adds a new on-premises listener connection in the Hybrid Connection Manager to an existing Hybrid Connection on [!INCLUDE[azure_2](/Token/azure_2_md.md)]. <br /> <br />|[-ConnectionString] &lt;your on-premises connection string&gt; <br /> <br />**Required**. Enter the complete on-premises connection string listed in the [!INCLUDE[azportal](/Token/azportal_md.md)]. Example includes: <br /> <br />add-hybridConnection -connectionString “Endpoint=hc://*YourBizTalkServiceName*.hybrid.biztalk.windows.net/*YourNewHybridConnectionName*;SharedAccessKeyName=defaultListener;SharedAccessKey=xxxx” <br /> <br />|
|Update-HybridConnection <br /> <br />|Updates the connectivity parameters for an on-premises listener configured on the local Hybrid Connection Manager. <br /> <br />|[-ConnectionString] &lt;your on-premises connection string&gt; <br /> <br />**Required**. Enter the complete on-premises connection string of the Hybrid Connection you want to change. Example includes: <br /> <br />update-hybridConnection -connectionString “Endpoint=hc://*YourBizTalkServiceName*.hybrid.biztalk.windows.net/*YourHybridConnectionName*;SharedAccessKeyName=defaultListener;SharedAccessKey=xxxx” <br /> <br />|
|Remove-HybridConnection <br /> <br />|Removes an on-premises listener for a specific Hybrid Connection from the local Hybrid Connection Manager. <br /> <br />|[-ConnectionString] &lt;your on-premises connection string&gt;   **OR** [-URI] &lt;HybridConnectionURI&gt; <br /> <br />**Required**. Only one of the two parameters must be entered. Enter the complete on-premises connection string of the Hybrid Connection or URI you want to remove. Examples include: <br /> <br />remove-HybridConnection -connectionString “Endpoint=hc://*YourBizTalkServiceName*.hybrid.biztalk.windows.net/*YourHybridConnectionName*;SharedAccessKeyName=defaultListener;SharedAccessKey=xxxx” <br /> <br />**OR** <br /> <br />remove-hybridConnection -URI “hc://*YourBizTalkServiceName*.hybrid.biztalk.windows.net/*YourHybridConnectionName*” <br /> <br />|
|Get-HybridConnection <br /> <br />|Returns information on the on-premises listeners for all the Hybrid Connections configured on the local Hybrid Connection Manager. <br /> <br />|[-ConnectionString] &lt;your on-premises connection string&gt;   **OR** [-URI] &lt;HybridConnectionURI&gt; <br /> <br />[-All] <br /> <br />[-format] ShowKeys <br /> <br />**Optional**. If no parameters are specified, all Hybrid Connections are returned. Example includes: <br /> <br />get-hybridConnection -URI “hc://*YourBizTalkServiceName*.hybrid.biztalk.windows.net/*YourHybridConnectionName*” <br /> <br />|
|Set-HybridConnectionManagerConfiguration <br /> <br />|Configures the local management TCP port for the Hybrid Connection Manager. <br /> <br />|[-ManagementPort] &lt;TCPPortNumber&gt; <br /> <br />**Required**. Example includes: <br /> <br />set-hybridConnectionManagerConfiguration -managementPort 9352 <br /> <br />This local port is used by the Hybrid Connection Manager to retrieve the status of the Hybrid Connections connected on the local machine. <br /> <br />|
