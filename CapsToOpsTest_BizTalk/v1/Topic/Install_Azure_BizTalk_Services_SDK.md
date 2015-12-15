---
description: na
keywords: na
pagetitle: Install Azure BizTalk Services SDK
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10873203-56b3-445c-8340-ef073f5365f8
---
# Install Azure BizTalk Services SDK
Steps to install [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] has three main components: Developer SDK, [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime, and [!INCLUDE[powershell](/Token/powershell_md.md)] cmdlet Tools. In this topic:

[BizTalk Service SDK Components Explained](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Components)

[Software Requirements](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Reqs)

[Install BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Installation)

[Upgrade from Preview to General Availability (GA)](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Upgrade)

[Migrate the BizTalk Adapter Service Runtime Environment](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Migrate)

[Remove BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Uninstall)

## <a name="BKMK_Components"></a>BizTalk Service SDK Components Explained
The following table lists the components within the [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK, and lists what gets installed:

|Component <br /> <br />|Details <br /> <br />|
|-------------|-----------|
|**Developer SDK** <br /> <br />|[Download BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057) <br /> <br />[Download schemas](http://go.microsoft.com/fwlink/p/?LinkId=235057) <br /> <br />On the **Development** computer with [!INCLUDE[vsprvs](/Token/vsprvs_md.md)], the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK is installed to develop and design your [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications. The Developer SDK automatically installs: <br /> <br /><ul><li>**BizTalk Service** project template in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] to create [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)]s. </li><li>**BizTalk Service Artifacts** project template in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] to create [!INCLUDE[transform](/Token/transform_md.md)]s and schemas. </li><li>[!INCLUDE[bap](/Token/bap_md.md)] 2013: Used if your [!INCLUDE[af_integration](/Token/af_integration_md.md)] application sends messages to on-premises line-of-business (LOB) systems including SAP, SQL Server, Siebel, Oracle Database, or Oracle E-Business Suite. **Note:**    Installs the [!INCLUDE[bap](/Token/bap_md.md)] 32-bit and 64-bit versions. </li><li>Microsoft WCF LOB Adapter SDK: Required by the Microsoft [!INCLUDE[bap](/Token/bap_md.md)]. </li><li>The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Server Explorer plug-in in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] to create [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s used by the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]. </li> </ul>|
|**Runtime** <br /> <br />|Using Internet Information Services (IIS), the **Runtime** computer manages connectivity between your [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] applications and the on-premises Line-of-Business (LOB) applications. **Important:** If your applications use an on-premises LOB system, then you must install the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime on a computer with IIS and internet access. If your application does **not** connect to an on-premises LOB system, then you do **not** need to install the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime. <br />This option automatically installs: <br /> <br /><ul><li>The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**Runtime** : Runs on-premises and uses WCF web services to manage the communication between the on-premises LOB systems and the [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications. </li><li>Microsoft WCF LOB Adapter SDK : Required by the Microsoft [!INCLUDE[bap](/Token/bap_md.md)] 2013 </li><li>[!INCLUDE[bap](/Token/bap_md.md)] 2013 : Used if your [!INCLUDE[af_integration](/Token/af_integration_md.md)] application sends messages to on-premises line-of-business (LOB) systems including SAP, SQL Server, Siebel, Oracle Database, or Oracle E-Business Suite. **Note:**    On a 64-bit computer, the [!INCLUDE[bap](/Token/bap_md.md)] 32-bit and 64-bit versions are installed. On a 32-bit computer, the [!INCLUDE[bap](/Token/bap_md.md)] 32-bit version is installed. </li><li>Windows Communication Foundation HTTP Activation feature (.NET Framework 3.5) </li><li>ASP.NET 4.5 feature (.NET Framework 4.5) </li><li>Internet Information Services (IIS) feature, including: <br /> <br /><ul><li>ASP.NET 3.5 </li><li>ASP.NET 4.5 </li><li>CGI </li><li>ISAPI Extensions </li><li>ISAPI Filters </li><li>Windows Authentication </li> </ul> </li><li>Windows Process Activation Service feature </li> </ul>[Runtime Components: BizTalk Adapter Service](/Topic/Runtime_Components__BizTalk_Adapter_Service.md) describes the architecture. <br /> <br />|
|**Tools** <br /> <br />|**Tools** includes the Windows PowerShell cmdlets to manage the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime components and your deployed [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications. Tools automatically installs: <br /> <br /><ul><li>**Windows PowerShell** extensions to manage the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime and the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. </li><li>Microsoft WCF LOB Adapter SDK : Required by the Microsoft [!INCLUDE[bap](/Token/bap_md.md)] 2013. </li><li>[!INCLUDE[bap](/Token/bap_md.md)] 2013 : Used if your [!INCLUDE[af_integration](/Token/af_integration_md.md)] application sends messages to on-premises line-of-business (LOB) systems including SAP, SQL Server, Siebel, Oracle Database, or Oracle E-Business Suite. **Note:**    On a 64-bit computer, the [!INCLUDE[bap](/Token/bap_md.md)] 32-bit and 64-bit versions are installed. On a 32-bit computer, the [!INCLUDE[bap](/Token/bap_md.md)] 32-bit version is installed. </li> </ul>|
> [!IMPORTANT]
> - The [!INCLUDE[bap](/Token/bap_md.md)] is automatically included with [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK and [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]. There is no separate installation or license needed.
> - The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Windows PowerShell module name is Microsoft.BizTalk.Adapter.Services.Powershell.dll. As a result, PowerShell scripts written using the Preview-version of the cmdlets may fail after upgrading.
> - A copy of the EULA is available in the Setup folder. It can be printed.

## <a name="BKMK_Reqs"></a>Software Requirements
Setup is separated into three environments: Development, Runtime, and Tools. The environments can be configured on a single computer or separate computers. For a complete installation, set up the [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] development and the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime/tools environments on the same computer. The following table lists the software requirements to install the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] environments on different computers:

|Software <br /> <br />|Details <br /> <br />|Computer <br /> <br />|
|------------|-----------|------------|
|Operating System <br /> <br />|Can be any of the following: <br /> <br /><ul><li>Windows 7 </li><li>Windows Server 2008 R2 </li><li>Windows 8 </li><li>Windows Server 2012 </li> </ul> **Important:** [!INCLUDE[vs2012](/Token/vs2012_md.md)] requires Windows 7 and Windows 2008 R2 [Service Pack 1](http://go.microsoft.com/fwlink/p/?LinkID=252370) to be installed. <br />|<ul><li>Development </li><li>Runtime </li><li>Tools </li> </ul>|
|[!INCLUDE[.NET_Framework_2nd](/Token/.NET_Framework_2nd_md.md)] <br /> <br />|Required versions include: <br /> <br /><ul><li>**.NET Framework 3.5.1**: <br /> <br />   Windows Server :  Open **Server Manager**, select **Features**, and select **.NET Framework 3.5**. <br /> <br />   Windows 7/Windows 8 : Open **Control Panel**, select **Programs And Features**, select **Turn Windows Feature On or Off**, and select **Microsoft .NET Framework 3.5**. </li><li>**.NET Framework 4.5**: <br /> <br />   Windows Server 2008 R2/Windows 7 : Download [Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/p/?LinkID=242919). <br /> <br />   Windows Server 2012/Windows 8 : In **Features**, select **.NET Framework 4.5 Advanced Services**. </li> </ul>|<ul><li>Development </li><li>Runtime </li><li>Tools </li> </ul>|
|Microsoft [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] 2012 <br /> <br />|Microsoft [!INCLUDE[csprcs](/Token/csprcs_md.md)] .NET is the minimum requirement. [Installing Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw%28v=vs.110%29.aspx) provides more information. **Important:** [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] 2012 Express editions (Web/Desktop) are not supported for [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK. <br />|<ul><li>Development </li> </ul>|
|LOB Server client libraries <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] requires the LOB Server client libraries to communicate with the LOB systems. So wherever you install the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)], also install the LOB client libraries. <br /> <br />If you don’t use or need the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)], then you don’t need to install the LOB Server client libraries. <br /> <br />The [BizTalk Server 2013 Installation Guides](http://go.microsoft.com/fwlink/p/?LinkID=269582) provides more specific details on what client libraries are required and where to install them from. <br /> <br />|<ul><li>Development </li><li>Runtime </li><li>Tools </li> </ul>|
|[!INCLUDE[sb2](/Token/sb2_md.md)] namespace <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] uses the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace and the [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name/Issuer Key values. When you create the LOB connections in your [!INCLUDE[vsprvs](/Token/vsprvs_md.md)] project, you enter these values. <br /> <br />See [How To: Create or Modify a Service Bus Service Namespace](http://msdn.microsoft.com/library/azure/hh690931.aspx). <br /> <br />|<ul><li>Development </li> </ul>|
|Internet Explorer <br /> <br />|Internet Explorer is used to access the [!INCLUDE[tpm_full](/Token/tpm_full_md.md)], which can be from any computer with internet access. Supported Internet Explorer versions include: <br /> <br /><ul><li>Internet Explorer 9 desktop </li><li>Internet Explorer 10 desktop </li><li>Internet Explorer 11 desktop </li> </ul> **Note:** The [!INCLUDE[tpm_full](/Token/tpm_full_md.md)] uses Silverlight. The Modern Browser versions of Internet Explorer are not supported. <br />|<ul><li>Runtime </li><li>Tools </li> </ul>|
|Internet access <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime starts a relay endpoint on [!INCLUDE[sb1](/Token/sb1_md.md)]. The computer and the account that runs the IIS website must have access to the Internet through the firewall. <br /> <br />Depending on your network requirements, you may need to install the Forefront TMG Client at [Forefront Threat Management Gateway (TMG) Client](http://go.microsoft.com/fwlink/p/?LinkId=303843). The TMG Client also supports ISA Server 2004 and ISA Server 2006. <br /> <br />|<ul><li>Runtime </li> </ul>|
|HTTP 1.1 through Proxy connections <br /> <br />|To connect to your namespace, HTTP 1.1 through Proxy connections is required. By default, HTTP 1.1 through Proxy connections is enabled. It can be enabled in Internet Explorer Options (Advanced tab), a domain group policy or enabling HTTP 1.1 on the proxy server. <br /> <br />|<ul><li>Runtime </li> </ul>|
|Windows PowerShell 3.0 <br /> <br />|Required to use the Windows PowerShell cmdlets. Installation options: <br /> <br />**Windows Server 2008 R2/Windows 7** : Download [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/p/?LinkId=251995). <br /> <br />**Windows Server 2012/Windows 8** : Automatically included with the operating system. There is no separate installation. <br /> <br />|<ul><li>Tools </li> </ul>|

## <a name="BKMK_Installation"></a>Install BizTalk Services SDK
**BEFORE YOU INSTALL**:

- **Close all instances of [!INCLUDE[vsprvs](/Token/vsprvs_md.md)]**. Terminate any MsBuild.exe processes; which can be done using Task Manager.

- **Update machine.config**: In previous [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK versions, you may have updated the machine.config file manually or by using *RelayConfigurationInstaller.exe /i*. If you updated the machine.config file, run *RelayConfigurationInstaller.exe /u* to remove the entries from the machine.config. The RelayConfigurationInstaller tool is available with your previous SDK version and the December 2012 Release. You must use the RelayConfigurationInstaller tool that shipped with your previous SDK version.

- **Upgrade**: You can run Setup to upgrade from a Preview version to the latest SDK version. If you prefer a fresh installation, uninstall any previous versions of the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK and the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]. [Removing the BizTalk Services SDK and BizTalk Adapter Service](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Uninstall) lists the uninstall steps.

- **Recommended installation**: A recommended installation spans at least two computers: Development and Runtime/Tools. When these components are installed on different computers, all the computers must be in a trusted network.

- **Runtime is optional**: If your [!INCLUDE[af_integration](/Token/af_integration_md.md)] application does not connect to an on-premises Line-of-Business (LOB) system, then you do not need the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime.

- **Install test certificate**: When you create a BizTalk Service using the [!INCLUDE[azportal](/Token/azportal_md.md)], a test certificate is automatically created and can be downloaded from the [!INCLUDE[azportal](/Token/azportal_md.md)]. You can use this certificate when installing the Runtime. [APPENDIX: BizTalk Services Certificates Overview](/Topic/APPENDIX__BizTalk_Services_Certificates_Overview.md) lists the steps to install the certificate on your local computer.

- **Open TCP port**: If you install the Runtime, it creates a web site in IIS that is bound to port 8080 (by default). On the IIS server, port 8080 must opened within any firewall. If you use Windows Firewall, create a new Inbound Rule on TCP port 8080. Steps listed at [How to create a Windows Firewall Inbound Rule](http://blogs.msdn.com/b/mandi/archive/2014/11/03/how-to-create-a-windows-firewall-inbound-rule.aspx).

- **Tools** can be installed on any computer (including multiple computers) that uses the [!INCLUDE[powershell](/Token/powershell_md.md)] cmdlets.

**INSTALL STEPS**

1. Log in with an account that is a member of the local Administrators group. If installing the **Runtime**, the account must also have administrative privileges on the IIS instance where you install the Runtime.

2. Install the [Software Requirements](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Reqs).

3. Run the 32-bit or 64-bit **WindowsAzureBizTalkServicesSetup.exe** as Administrator.

   > [!NOTE]
   > If User Account Control is enabled, an alert to install may display. Select **Yes** and proceed with the installation.

4. Accept the license agreement and select **Next**.

5. Select **Developer SDK**, **Runtime**, and/or **Tools** depending on your needs. [BizTalk Service SDK Components Explained](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Components) lists the differences. Select **Next**.

6. **Summary** lists the Setup actions. Select **Install**.

   > [!NOTE]
   > For a fresh installation, the Setup action is **Install**. If some components are already installed, **Summary** lists the versions and the Setup action; like **None** or **Upgrade**. [Upgrade from Preview to General Availability (GA)](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Upgrade) provides more information.

7. **If you select Runtime**, the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] setup starts:

   1. Select **Next** on the Welcome page.

   2. Accept the license agreement and select **Next**.

   3. For the Application Pool, enter an identity that has Internet access and select **Next**.

      The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] application pool in IIS is created and executes as this identity. Internet access is needed because this identity is used to access the relay endpoints on the [!INCLUDE[sb2](/Token/sb2_md.md)].

   4. In **Azure BizTalk Services Deployment Details**, enter the [!INCLUDE[af_integration](/Token/af_integration_md.md)] deployment URL, and select **Next**.

      This URL is used to ascertain the artifact store associated with your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. The configuration settings for [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] components you create, such as [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s, are stored in the artifact store.

   5. Select the certificate bindings for the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] website and select **Next**.

      - **Use SSL to secure the management service**: Select this option to encrypt the HTTP requests with SSL.

      - **Select an existing SSL certificate**: Select this option to select an existing certificate from the Certificates store. The certificate should be from a trusted certificate authority.

      - **Port**: Enter the port number for the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] website. By default, port 8080 is entered. Confirm the port is open in your firewall.

   6. Select **Install**. When the wizard completes, select **Finish** to go back to the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK wizard.

8. Select **Finish** to complete the installation and exit the wizard.

When the installation completes, a setup log file is created in the user’s temp directory at C:\Users\*UserName*\AppData\Local\Temp. If the installation fails, refer to this log file for any errors. If the installation succeeds, you have an environment with all the components needed to create and/or manage [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications.

## <a name="BKMK_Upgrade"></a>Upgrade BizTalk Services SDK to the latest version
You can upgrade the Developer, Runtime, and Tools components from [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] Preview or [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] (November 2013) General Availability (GA) to the latest version. To upgrade, run **WindowsAzureBizTalkServicesSetup.exe** as Administrator, select the components you want to upgrade, and continue with the setup. The Setup detects the versions of the previous installed components, and suggests upgrading them accordingly. Typically, you must have all the three components installed with the same version. For example, if you have Developer SDK and Runtime installed of one version, and the Tools component installed of another version, the setup would recommend that all the components should be of the same version.

During the upgrade, your existing artifacts are upgraded to GA, including [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] artifacts, [!INCLUDE[transform](/Token/transform_md.md)]s, and [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] components. Also, if you choose to upgrade the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime component, the setup also performs a migration of [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] settings from an on-premises SQL Server database to [!INCLUDE[azure_1](/Token/azure_1_md.md)] storage. For more information, see [Migrate the BizTalk Adapter Service Runtime Environment](/Topic/Install_Azure_BizTalk_Services_SDK.md#BKMK_Migrate).

**Post Upgrade**

After you upgrade to the latest version, do the following:

- Redeploy EDI Agreements that have Batching enabled. If Batching is not used in the Agreement, there is no need to redeploy the EDI Agreement.

- The BizTalk Adapter Service Windows PowerShell module name is Microsoft.BizTalk.Adapter.Services.Powershell.dll. As a result, PowerShell scripts written using the Preview-version of the cmdlets may fail after upgrading. These scripts must be rewritten.

- Refer to [Release Notes for Azure BizTalk Services](/Topic/Release_Notes_for_Azure_BizTalk_Services.md) for additional issues that can occur after upgrading.

- As a best practice, create a backup of the BizTalk Service. [BizTalk Services: Backup and Restore](http://go.microsoft.com/fwlink/p/?LinkID=329873) provides more information on creating a backup.

## <a name="BKMK_Migrate"></a>Migrate the BizTalk Adapter Service Runtime Environment
The Preview and the November 2013 GA version of [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] component, available as part of [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK, required an on-premises SQL Server database for storing information about [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. The February 2014 version of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] component stores the information in the repository associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK setup enables you to migrate the information stored in the on-premises SQL Server database to the [!INCLUDE[azure_1](/Token/azure_1_md.md)] storage associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. The following steps provide information on how to perform the migration:

> [!NOTE]
> You can perform the migration along with the upgrade.

1. On a computer that has a previous version of [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] installed, run the **WindowsAzureBizTalkServicesSetup.exe** as an administrator.

   > [!NOTE]
   > If User Account Control is enabled, an alert to install may display. Select **Yes** and proceed with the installation.

2. Accept the license agreement and select **Next**.

3. Select **Runtime** and then select **Next**.

4. The **Summary** page lists that the Runtime ([!INCLUDE[lobconnect](/Token/lobconnect_md.md)]) component will be upgraded. Select **Next**.

5. On the **Migration** page, provide the URL for your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription, Access Control namespace associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)], and the issuer name/issuer key for the Access Control namespace.

   > [!NOTE]
   > The setup uses the URL to ascertain the repository associated with your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. The configuration settings for [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] components you create, such as [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s and [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s, are stored in the repository associated with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. If you used [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] as part of your existing [!INCLUDE[af_integration](/Token/af_integration_md.md)] applications created using the Preview or November 2013 GA version of the SDK, the wizard migrates the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] configuration settings from the local SQL Server database to the repository associated with the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription.

   Select **Install**.

6. After the wizard completes, select **Finish**.

## <a name="BKMK_Uninstall"></a>Remove BizTalk Services SDK
[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK and [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] can be uninstalled using the Control Panel. Select **Uninstall a Program**. In the **Uninstall or change a program** page, right-click the component, and select **Uninstall**. The complete list of the installed components includes:

- [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK

- removed by Jason Zhu, due to bug 482925

- Windows Communication Foundation LOB Adapter SDK (WCF LOB Adapter SDK), if installed

   > [!IMPORTANT]
   > Always uninstall the [!INCLUDE[bap](/Token/bap_md.md)] before you uninstall the WCF LOB Adapter SDK.

## See Also
[BizTalk Services](/Topic/BizTalk_Services.md)

