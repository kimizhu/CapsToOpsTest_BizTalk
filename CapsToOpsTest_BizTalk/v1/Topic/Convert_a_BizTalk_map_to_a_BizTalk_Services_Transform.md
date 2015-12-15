---
description: na
keywords: na
pagetitle: Convert a BizTalk map to a BizTalk Services Transform
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 38fb7395-6172-4e5d-89c7-c84263387ca0
---
# Convert a BizTalk map to a BizTalk Services Transform
A command line tool that converts [!INCLUDE[btsBizTalkServerNoVersion](/Token/btsBizTalkServerNoVersion_md.md)] maps to [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)][!INCLUDE[transform](/Token/transform_md.md)]s/maps.

## BizTalk Map Migration Tool
The **BizTalk Map Migration Tool** is available in the **Tools** package provided with the [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK and can be downloaded from [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057).

If an existing BizTalk environment contains maps and functoids, the **BTM Migration Tool** can help migrate these artifacts to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. The **BTM Migration Tool** is a command line tool that uses the following parameters:

- A BizTalk map (.btm)

- Optional. A resulting [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)][!INCLUDE[transform](/Token/transform_md.md)] (.trfm)

## Prerequisites
The following items must be installed on the same computer where you run the tool:

- BizTalk Server 2010 or newer versions

- [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK

> [!IMPORTANT]
> If the tools fails, confirm [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] is listed at C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\Extensions\Microsoft.

## Usage

1. Copy the files and schemas associated with the BizTalk map (.btm) to the BtmToTrfmConvertor.exe folder.

2. Open a command window and go to the BtmToTrfmConvertor.exe folder.

3. Enter the following syntax:

   ```
   BtmToTrfmConvertor.exe BTMFilePathOutputTrfm
   ```
   For example, enter the following:

   ```
   BtmToTrfmConvertor.exe c:\BizTalkFiles\CustomerInput.btm C:\Transforms\Output.trfm
   ```
   If you do not enter the output parameter, a .trfm file is created in the same directory and with the same name as the input .btm file.

## Limitations
The BTM Migration Tool does not migrate all the functoids from the BizTalk Server map. For a list of limitations and known issues with the tool, refer to the readme in the tools package.

## See Also
[Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md)
[Learn and create Message Maps and Transforms](/Topic/Learn_and_create_Message_Maps_and_Transforms.md)

