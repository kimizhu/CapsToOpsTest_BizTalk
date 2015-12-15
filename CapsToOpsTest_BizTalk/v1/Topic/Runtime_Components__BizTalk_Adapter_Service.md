---
description: na
keywords: na
pagetitle: Runtime Components: BizTalk Adapter Service
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 355e839a-c2ca-48e2-bc2e-e3cd1ad32466
---
# Runtime Components: BizTalk Adapter Service
When [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] runtime is installed, the following components are created:

- [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] web site in IIS

- Configuration store in [!INCLUDE[azure_1](/Token/azure_1_md.md)]

To install and setup the Runtime, refer to [Install Azure BizTalk Services SDK](/Topic/Install_Azure_BizTalk_Services_SDK.md).

## [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] web site
The **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site and **BizTalk Adapter AppPool** are created in IIS. The **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site contains the following:

|||
|-|-|
|BAService <br /> <br />|An application that hosts the Management API that runs in the ManagementService.svc WCF web service. This WCF web service runs continuously monitoring the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. <br /> <br />The ManagementService.svc WCF web service uses a web.config file in the *\Program Files\Microsoft BizTalk Adapter Service\BAService* folder. <br /> <br />|
|[!INCLUDE[lobrelay](/Token/lobrelay_md.md)] <br /> <br />|When a LOB component is added, an application with the same name is also created. This application hosts the RuntimeService.svc WCF web service. A runtime service is created for *every* LOB component in the [!INCLUDE[msgflow](/Token/msgflow_md.md)] application. So if there are 15 LOB components in the [!INCLUDE[msgflow](/Token/msgflow_md.md)] application, there will be at least 15 RuntimeService.svc WCF web services IIS. <br /> <br />The RuntimeService.svc WCF web service uses a web.config file in the *\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime* folder. <br /> <br />|
Windows Authentication is specified for the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site and the **BAService** application hosted in this web site.

By default, the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site binds to port 8080. This port is set during the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] setup and can also be modified in the web site in IIS.

### Reconnect Interval
By default, an IIS application pool is configured to recycle every 1740 seconds (29 minutes). When the **BizTalk Adapter AppPool** recycles, a [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] may fail to start. If a [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] fails to start, an attempt is made to restart the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] after a fixed interval. This is controlled by the **ReConnectIntervalInSeconds** property, which has a default value of 30 seconds.

To change or disable the reconnect interval:

1. Open the **Internet Information Services (IIS) Manager**.

2. Expand **Sites** and expand **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**.

3. Click **BAServiceRuntime**. Under the ASP.NET group, click **Application Settings** and click **Open Feature** in the Actions pane.

4. To modify the reconnect interval, click **ReConnectIntervalInSeconds** and click **Edit** in the Actions pane. Set this to any value in seconds. For example, to set the reconnect interval to 5 minutes, enter 300. To disable the reconnect interval, set **ReConnectIntervalInSeconds** to any negative number, like **-1**.

**ReConnectIntervalInSeconds** can also be modified in the web.config file (*\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime*):

```
<appSettings>
    <add key="EnablePerfCounters" value="True" />
    <add key="ReConnectIntervalInSeconds" value="30" />
</appSettings>
```
> [!NOTE]
> The Recycling Settings in IIS can be configured. See [Configuring Recycling Settings for an Application Pool (IIS 7)](http://go.microsoft.com/fwlink/?LinkId=235317).

### Administrators can make client requests to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] web site
Users in the local Administrators group can make client requests to the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site within IIS. The **BAService** application inherits the **.NET Authorization Rules** from the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site and the web server-level.

To allow non-Administrators to make client requests to the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site, use the .NET Authorization Rules feature within IIS:

1. Open the **Internet Information Services (IIS) Manager**.

2. Expand **Sites** and click **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**.

3. Under the ASP.NET group, double-click **.NET Authorization Rules**. [NET Authorization Rules Page](http://go.microsoft.com/fwlink/?LinkId=229181) explains the UI elements.

4. In the Actions pane, click **Add Allow Rule**. [Add or Edit Allow Authorization Rule and Add or Edit Deny Authorization Rule Dialog Boxes](http://go.microsoft.com/fwlink/?LinkId=229182) explains the UI options when **Add Allow Rule** or **Add Deny Rule** is used.

> [!NOTE]
> When **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime** is installed, the identity specified during the Setup can make client requests to the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site. This identity also has permissions to access the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] configuration store.

## Configuration Store
The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] configuration is stored in [!INCLUDE[azure_1](/Token/azure_1_md.md)] using your [!INCLUDE[af_integration](/Token/af_integration_md.md)] URL you specify during the setup.

When an item is created in Server Explorer in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] on the development environment, the store is updated. [Connect to LOB systems from a BizTalk Services Project](/Topic/Connect_to_LOB_systems_from_a_BizTalk_Services_Project.md) provides details on Server Explorer and the development experience.

## See Also
[Development and Runtime Architecture: BizTalk Adapter Service](/Topic/Development_and_Runtime_Architecture__BizTalk_Adapter_Service.md)
[Connect to LOB systems from a BizTalk Services Project](/Topic/Connect_to_LOB_systems_from_a_BizTalk_Services_Project.md)
[PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md)
[LOB Security in BizTalk Adapter Service](/Topic/LOB_Security_in_BizTalk_Adapter_Service.md)
[Troubleshoot the BizTalk Adapter Service](/Topic/Troubleshoot_the_BizTalk_Adapter_Service.md)
[Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md)

