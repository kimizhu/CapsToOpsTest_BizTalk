---
description: na
keywords: na
pagetitle: Clear-AzureBizTalkTrackingStore
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2d0b480-0587-4b40-bef6-1e3d751492bd
---
# Clear-AzureBizTalkTrackingStore
The **Clear-AzureBizTalkTrackingStore** clears the tracking store for your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

## Syntax
`Clear-AzureBizTalkTrackingStore -Sql <sqlstring> -AzureStore <azurestring> -Ndays <ndays> [DeleteAS2NRR] [-NoPrompt] [<CommonParameters>]`

## Parameters

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-Sql *&lt;SqlString&gt;* <br /> <br />|Required <br /> <br />|The SQL connection string to the tracking store. <br /> <br />|
|-AzureStore *&lt;azurestring&gt;* <br /> <br />|Required <br /> <br />|The [!INCLUDE[azure_1](/Token/azure_1_md.md)] storage account connection string. <br /> <br />|
|-Ndays *&lt;ndays&gt;* <br /> <br />|Required <br /> <br />|The number of days for which the tracking store data must be persisted, which means data older than the specified number of days is deleted. The minimum value must be 1. <br /> <br />|
|DeleteAS2NRR <br /> <br />|Optional <br /> <br />|Specify true if you want to delete the AS2 NRR data as well. Otherwise, specify false. <br /> <br />|
|[-NoPrompt] <br /> <br />|Optional <br /> <br />|If included, you are not prompted for a confirmation before the data is deleted from the store. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

## Examples

- **Successfully clear the tracking store**

   `Clear-AzureBiztalkTrackingStore -Sql (Get-Content sqlString.txt) -AzureStore (Get-Content AzureStore.txt) -Ndays 2 true -NoPrompt`

   *Output*

   ```
   Tracking records older than 2 days were purged successfully. 
   Active Batch records were cleaned successfully.
   Size of Tracking Store before purge: 5GB
   Size of Tracking Store after purge: 4.2GB
   Size of Archiving data purged: 300MB
   ```

- **Error when the specified URL does not exist**

   `Clear-AzureBiztalkTrackingStore -Sql ( Get-Content sqlString.txt) -AzureStore (Get-Content AzureStore.txt) -Ndays 2 true -NoPrompt`

   *Output*

   ```
   Unable to connect to tracking or archiving store. Please check the URL and try again.
   ```

## See Also
[PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md)

