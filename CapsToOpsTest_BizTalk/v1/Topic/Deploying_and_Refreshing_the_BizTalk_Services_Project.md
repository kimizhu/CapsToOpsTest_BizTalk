---
description: na
keywords: na
pagetitle: Deploying and Refreshing the BizTalk Services Project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b11dcdab-b270-4568-9df8-83852826c441
---
# Deploying and Refreshing the BizTalk Services Project
This section provides information about deploying a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] on to the [!INCLUDE[sb1](/Token/sb1_md.md)]. [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides you with the following deployment options:

[Deploy the project using Visual Studio](/Topic/Deploying_and_Refreshing_the_BizTalk_Services_Project.md#BKMK_DeployProject)

[Refresh the Deployment](/Topic/Deploying_and_Refreshing_the_BizTalk_Services_Project.md#BKMK_RefreshProject)

## <a name="BKMK_DeployProject"></a>Deploy the project using Visual Studio
An entire [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] includes the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]s that are part of the project as well as all the artifacts used in the project (schemas and transforms). This option is applicable if you are using the Visual Studio [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] template to create your message flow. Using the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], you can deploy the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]s as well as the artifacts (schemas and transforms), all at the same time.

#### To deploy a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

1. In Visual Studio, right-click the BizTalk Service solution and click **Build**.

2. After a successful build, right-click the solution name again, and then click **Deploy** to open the **&lt;&#42;project name&#42;&gt; Deployment** dialog box, and specify the following properties.

   |Property Name <br /> <br />|Description <br /> <br />|
   |-----------------|---------------|
   |**Deployment Endpoint** <br /> <br />|A read-only field that displays the BizTalk Service URL and the default namespace specified in [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. <br /> <br />|
   |**Acs Namespace** <br /> <br />|Specify the ACS namespace for [!INCLUDE[af_integration](/Token/af_integration_md.md)]. <br /> <br />|
   |**Issuer Name** <br /> <br />|Specify the username who is the owner of the service namespace you specified, or has manage claims to the namespace. This property is required to authenticate the identity of the user to the [!INCLUDE[sb2](/Token/sb2_md.md)]. <br /> <br />|
   |**Shared Secret** <br /> <br />|Specify the secret key for authentication of the service namespace owner. <br /> <br />|
   |**Refresh service after deploy** <br /> <br />|When redeploying the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] that contains updated user assemblies, check this option to refresh the service. Refreshing the services deploys the newer assemblies without redeploying the project. **Important:** During the refresh, the service is unavailable for approximately five minutes. <br />|

3. Click **Deploy**. The Visual Studio Output pane displays the deployment progress and result. The URL where the [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] is deployed is also displayed in the Output pane. You can also see and manage the deployed bridges in the **Bridges** tab of the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. See [Manage your Resources in BizTalk Services portal](/Topic/Manage_your_Resources_in_BizTalk_Services_portal.md) for more information.

   > [!IMPORTANT]
   > After you have deployed the project, you can start sending messages to the endpoint URL for the bridge. Note that the bridge enforces a timeout of 5 minutes when receiving messages from a client application.

## <a name="BKMK_RefreshProject"></a>Refresh the Deployment
After the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] is deployed, you can “refresh” the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. The Refresh Service option does the following:

- Deploys updated assembly files; which includes assemblies typically used with [!INCLUDE[transform](/Token/transform_md.md)] and [!INCLUDE[bridge](/Token/bridge_md.md)] files.

- Does not redeploy the entire [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]: Only deploys the newer and updated artifacts.

- Minimal downtime: During the refresh, the [!INCLUDE[af_integration](/Token/af_integration_md.md)] is unavailable for approximately five minutes.

There are two ways to refresh [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]:

- [Refresh using Visual Studio](/Topic/Deploying_and_Refreshing_the_BizTalk_Services_Project.md#BKMK_RefreshVS)

-

### <a name="BKMK_RefreshVS"></a>Refresh using Visual Studio
When you deploy the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], a Deployment dialog window displays with the **Refresh service after deploy** option. Check **Refresh service after deploy** to redeploy newer and updated assembly files (*FileName*.dll). To redeploy the entire [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], do not check **Refresh service after deploy**.

### <a name="BKMK_RefreshPS"></a>Refresh using Windows PowerShell
After you deploy the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], Windows PowerShell can be used to refresh [!INCLUDE[af_integration](/Token/af_integration_md.md)]; which redeploys newer and updated assembly files (*FileName*.dll).

To refresh [!INCLUDE[af_integration](/Token/af_integration_md.md)] in Windows PowerShell:

1. Install Windows PowerShell 3.0:

   |||
   |-|-|
   |Windows 8 <br /> <br />Windows Server 2012 <br /> <br />|Included with the operating system. <br /> <br />|
   |Windows 7 Service Pack 1 <br /> <br />Windows Server 2008 R2 Service Pack 1 **Important:** Service Pack 1 is required. <br />|PowerShell 1.0 is included with the operating system. PowerShell 3.0 is required and is included in the Windows Management Framework 3.0 download: <br /> <br />[Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) (http://www.microsoft.com/download/details.aspx?id=34595) <br /> <br />|

2. Open Windows PowerShell in an elevated mode: Start menu, **All Programs**, **Accessories**, **Windows PowerShell**.

3. In the Windows PowerShell window, import the module by typing the following:

   ```powershell
   import-module "C:\Program Files\Azure BizTalk Services SDK\Microsoft.BizTalk.Services.Powershell.dll"
   ```

4. In the Windows PowerShell window, use the **Restart-AzureBizTalkService** cmdlet to refresh the deployment. For more information, see [Restart-AzureBizTalkService](/Topic/Restart-AzureBizTalkService.md).

## See Also
[Create Rich Messaging Endpoints on Azure](/Topic/Create_Rich_Messaging_Endpoints_on_Azure.md)

