---
description: na
keywords: na
pagetitle: Development and Runtime Architecture: BizTalk Adapter Service
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2360e515-3493-4c35-92dc-87b587520697
---
# Development and Runtime Architecture: BizTalk Adapter Service
This topic describes the different parts of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. Specifically:

- [Development](/Topic/Development_and_Runtime_Architecture__BizTalk_Adapter_Service.md#BKMK_Development)

- [Runtime](/Topic/Development_and_Runtime_Architecture__BizTalk_Adapter_Service.md#BKMK_Runtime)

- [Process Flow](/Topic/Development_and_Runtime_Architecture__BizTalk_Adapter_Service.md#BKMK_ProcFlow)

**BEFORE YOU BEGIN**

There are two terms that are very important to understand:

|||
|-|-|
|[!INCLUDE[lobtarget](/Token/lobtarget_md.md)] <br /> <br />|An [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is your on-premises Line-of-Business (LOB) system and the operations (like SELECT or INSERT) exposed to your client applications. Specifically, the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] controls the LOB system connection URI (for example, mssql://SQLServerName:1433//myDatabase), the schema operation (for example, SELECT), and connection credentials (for example, myUserName and myPassword). <br /> <br />An [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] can be used by multiple LOB systems and is hosted in a [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. <br /> <br />|
|[!INCLUDE[lobrelay](/Token/lobrelay_md.md)] <br /> <br />|An [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] is a URL that provides a connection to the cloud using [!INCLUDE[sb2](/Token/sb2_md.md)] Relays. A [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] acts as a container for the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s and can be used with multiple [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. <br /> <br />|
A single [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] can be used with multiple [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. This is cost-effective because you can connect to a LOB system and execute an operation using one endpoint. There are restrictions based on the security model. As a best practice, group the same security method in one [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. For example, use the same [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] to host the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s that use message security.

> [!NOTE]
> When you create Line-of-Business (LOB) artifacts, these items are stored in a [!INCLUDE[azure_1](/Token/azure_1_md.md)] Storage account.

## <a name="BKMK_Development"></a>Development
Developing applications is done on-premises. On the Development environment, the application developer uses [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] to create the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] application that includes a Line-of-Business (LOB) component, like SQL Server. Specifically, the Development environment utilizes the following components:

- [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] to create a [!INCLUDE[msgflow](/Token/msgflow_md.md)]

- The LOB system client libraries (if applicable)

[Create the project in Visual Studio](/Topic/Create_the_project_in_Visual_Studio.md) provides information on creating a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. [Connect to LOB systems from a BizTalk Services Project](/Topic/Connect_to_LOB_systems_from_a_BizTalk_Services_Project.md) provides information on adding a LOB component to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

## <a name="BKMK_Runtime"></a>Runtime
The Runtime computer hosts the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime on-premises. The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime does the following:

- Manages on-premises to cloud connectivity.

- Supports multiple on-premises LOB systems using the adapters in the [!INCLUDE[bap](/Token/bap_md.md)].

- Routes to the different on-premises LOB systems using the adapters in the [!INCLUDE[bap](/Token/bap_md.md)].

[Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) provides information on setting up the Runtime environment and the different components.

## <a name="BKMK_ProcFlow"></a>Process Flow

1. On-premises, a [!INCLUDE[msgflow](/Token/msgflow_md.md)] application contains a [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] and is deployed to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] Portal. When deployed, the following occurs:

   - A [!INCLUDE[sb2](/Token/sb2_md.md)] endpoint is created using your Service Namespace.

   - On the Runtime server on-premises, the Runtime monitors the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] in [!INCLUDE[sb2](/Token/sb2_md.md)].

   [Deploying and Refreshing the BizTalk Services Project](/Topic/Deploying_and_Refreshing_the_BizTalk_Services_Project.md) provides the details on deployment.

2. When a message is received by the [!INCLUDE[msgflow](/Token/msgflow_md.md)] application, the [!INCLUDE[sb2](/Token/sb2_md.md)] endpoint passes the message to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] in [!INCLUDE[sb2](/Token/sb2_md.md)]. On the on-premises Runtime server, the following occurs:

   - The runtime service confirms the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] details in the configuration store hosted in the [!INCLUDE[azure_1](/Token/azure_1_md.md)] Storage account.

   - The runtime service executes the LOB operation (like INSERT or DELETE). A runtime WCF web service is created for every [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. So if there are 15 [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s in the [!INCLUDE[msgflow](/Token/msgflow_md.md)] application, there will be at least 15 runtime WCF web services.

3. When the LOB operation completes on the on-premises LOB system, the response is sent back to the Runtime service, goes to the [!INCLUDE[sb2](/Token/sb2_md.md)] endpoint and is passed to the [!INCLUDE[msgflow](/Token/msgflow_md.md)] application in [!INCLUDE[sb2](/Token/sb2_md.md)].

## See Also
[Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md)
[Connect to LOB systems from a BizTalk Services Project](/Topic/Connect_to_LOB_systems_from_a_BizTalk_Services_Project.md)
[PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md)
[LOB Security in BizTalk Adapter Service](/Topic/LOB_Security_in_BizTalk_Adapter_Service.md)
[Troubleshoot the BizTalk Adapter Service](/Topic/Troubleshoot_the_BizTalk_Adapter_Service.md)
[Create the project in Visual Studio](/Topic/Create_the_project_in_Visual_Studio.md)
[Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md)

