---
description: na
keywords: na
pagetitle: Connect to LOB systems from a BizTalk Services Project
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-12-07
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a79422-dad0-43ae-b2b4-99f0a8657ada
---
# Connect to LOB systems from a BizTalk Services Project
Connect to the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)].

The application developer uses the development environment to build the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] application and deploy to the [!INCLUDE[sb2](/Token/sb2_md.md)]. When [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] is installed, the components used to create the [!INCLUDE[af_integration](/Token/af_integration_md.md)] application with LOB connectivity are available.

To configure the Development environment, see to [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md)

## Server Explorer
Server Explorer in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] is used to create the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. Server Explorer is available on the **View** menu in your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)].

> [!IMPORTANT]
> [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] must be opened with Administrative privileges to create and develop with the LOB adapters.

### Add your Management URL
To create a [!INCLUDE[lobtarget](/Token/lobtarget_md.md)], connect to your Runtime server:

1. Create the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)]. [Get started with a Visual Studio project](/Topic/Get_started_with_a_Visual_Studio_project.md) lists the steps.

2. In **Server Explorer**, right-click **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**, and select **Add BizTalk Adapter Service**. This prompts for the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management URL:

   ![](/Image/AI_AddSBConnectServer.jpg)

   The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management URL is path to the ManagementService.svc WCF service hosted in IIS. [Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) provides more information on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] components within IIS.

   If the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime is installed locally with the default settings, enter:

   **http://localhost:8080/BAService/ManagementService.svc/**

   Or

   **https://localhost:8080/BAService/ManagementService.svc/**

   If the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime is installed remotely with the default settings, enter:

   **http://&#42;ServerName&#42;:8080/BAService/ManagementService.svc/**

   Or

   **https://&#42;ServerName&#42;:8080/BAService/ManagementService.svc/**

   During the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] installation, you choose whether to allow SSL connections. The runtime URL automatically defaults to HTTP or HTTPS depending on your SSL choice. In the following scenarios, you may need to change from the default settings:

   - You installed the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] with the no SSL option. From another computer, you connect to the Runtime URL. In this scenario, you must enter HTTP for the Runtime URL:

      http://*ServerName*:8080/BAService/ManagementService.svc/

   - You installed the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] locally and allowed SSL connections. You reinstall the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] and don’t allow SSL connections. In this scenario, you must enter HTTP for the Runtime URL:

      http://localhost:8080/BAService/ManagementService.svc/

   > [!IMPORTANT]
   > The web site and BAService application in IIS use Windows Authentication. If you enter the fully qualified domain name (FQDN) of this IIS server, you are prompted for authentication credentials when browsing.

3. Select **OK**. This adds the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server in the Server Explorer and the LOB Types installed with the [!INCLUDE[bap](/Token/bap_md.md)].

   > [!NOTE]
   > Depending on the SSL and certificate options chosen during the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] setup, you may get a **server certificate for the website may not be valid** error. This typically happens if the certification authority is not trusted. If you chose to create a new self-signed certificate, this error is expected. Proceed to the website.

4. Expand the server URL and **LOB Types** to see the individual LOB adapters installed with the [!INCLUDE[bap](/Token/bap_md.md)]. When prompted, enter the [!INCLUDE[ac2](/Token/ac2_md.md)] namespace and issuer name/issuer key values.

   > [!NOTE]
   > The [!INCLUDE[ac2](/Token/ac2_md.md)] values are listed in the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkId=517414). Select your BizTalk Service and then select **Connection Information**. You can copy and paste these values.

To configure the individual [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s, refer to the Line-of-Business (LOB) system:

[Connect to Oracle Database or eBusiness Suite in a BizTalk Services Project](/Topic/Connect_to_Oracle_Database_or_eBusiness_Suite_in_a_BizTalk_Services_Project.md)

[Connect to mySAP Business Suite in a BizTalk Services Project](/Topic/Connect_to_mySAP_Business_Suite_in_a_BizTalk_Services_Project.md)

[Connect to SQL Server in a BizTalk Services Project](/Topic/Connect_to_SQL_Server_in_a_BizTalk_Services_Project.md)

[Connect to Siebel eBusiness Applications in a BizTalk Services Project](/Topic/Connect_to_Siebel_eBusiness_Applications_in_a_BizTalk_Services_Project.md)

## See Also
[Connect to Oracle Database or eBusiness Suite in a BizTalk Services Project](/Topic/Connect_to_Oracle_Database_or_eBusiness_Suite_in_a_BizTalk_Services_Project.md)
[Connect to mySAP Business Suite in a BizTalk Services Project](/Topic/Connect_to_mySAP_Business_Suite_in_a_BizTalk_Services_Project.md)
[Connect to SQL Server in a BizTalk Services Project](/Topic/Connect_to_SQL_Server_in_a_BizTalk_Services_Project.md)
[Connect to Siebel eBusiness Applications in a BizTalk Services Project](/Topic/Connect_to_Siebel_eBusiness_Applications_in_a_BizTalk_Services_Project.md)
[Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md)

