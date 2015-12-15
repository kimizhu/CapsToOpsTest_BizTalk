---
description: na
keywords: na
pagetitle: LOB Security in BizTalk Adapter Service
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe5e679e-5a9f-4999-83dc-cd23cf90bdea
---
# LOB Security in BizTalk Adapter Service
In [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] security refers to authentication with [!INCLUDE[msgflow](/Token/msgflow_md.md)] cloud application and the on-premises Line-of-Business (LOB) systems. Authentication credentials are specified during Design time and Runtime.

## Design Time Security
[!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] is used to create and add [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] project. This process creates web services in IIS, writes data to the back-end Configuration Store database, and connects to the LOB system. As a result, you must do the following:

- Open [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] with Administrative privileges

- Join the local Administrators group

- removed by Jason Zhu, due to bug 482925

- Get the System Administrator right on the on-premises source LOB system

When a [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is added to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] project in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)], the Connection can be configured using one of the following options:

- Windows Authentication

- User name and password

> [!NOTE]
> Not all options may be available for the individual LOB adapters.

These credentials are used to connect to the LOB system, retrieve the metadata and perform operations like INSERT or DELETE. These credentials will then create a [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] by selecting an operation. The individual LOB components provide more information on creating the Connection:

[Connect to Oracle Database or eBusiness Suite in a BizTalk Services Project](/Topic/Connect_to_Oracle_Database_or_eBusiness_Suite_in_a_BizTalk_Services_Project.md)

[Connect to mySAP Business Suite in a BizTalk Services Project](/Topic/Connect_to_mySAP_Business_Suite_in_a_BizTalk_Services_Project.md)

[Connect to Siebel eBusiness Applications in a BizTalk Services Project](/Topic/Connect_to_Siebel_eBusiness_Applications_in_a_BizTalk_Services_Project.md)

[Connect to SQL Server in a BizTalk Services Project](/Topic/Connect_to_SQL_Server_in_a_BizTalk_Services_Project.md)

## Runtime Security
Runtime authentication occurs when a message is sent through the [!INCLUDE[sb2](/Token/sb2_md.md)] (on the cloud) to the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime (on-premises) and then to the LOB system (on-premises). The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] supports the following security mechanisms:

|||
|-|-|
|Fixed Username <br /> <br />|The username and password specified when the Connection is configured. These credentials will persist and connect to the LOB system when a message for that [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is received. Select this option if you are using a username and password created locally on the LOB system. <br /> <br />|
|Fixed Windows Credentials <br /> <br />|The username and password specified when the Connection is configured. These credentials will persist and connect to the LOB system when a message for that [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is received. Select this option to use a Windows domain account. <br /> <br />|
|Custom SOAP Header <br /> <br />|The logon credentials are part of the message using a SOAP header. <br /> <br />|
|Message Credential <br /> <br />|The logon credentials are part of the message using a standard web service header. <br /> <br />|
> [!NOTE]
> Not all options may be available for the individual LOB adapters.

To specify the Runtime security, configure the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)]. The individual LOB components provide more information on creating a [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]:

[Connect to Oracle Database or eBusiness Suite in a BizTalk Services Project](/Topic/Connect_to_Oracle_Database_or_eBusiness_Suite_in_a_BizTalk_Services_Project.md)

[Connect to mySAP Business Suite in a BizTalk Services Project](/Topic/Connect_to_mySAP_Business_Suite_in_a_BizTalk_Services_Project.md)

[Connect to Siebel eBusiness Applications in a BizTalk Services Project](/Topic/Connect_to_Siebel_eBusiness_Applications_in_a_BizTalk_Services_Project.md)

[Connect to SQL Server in a BizTalk Services Project](/Topic/Connect_to_SQL_Server_in_a_BizTalk_Services_Project.md)

## Additional Security Precautions

### Enable HTTP 1.1 through Proxy
When using a Proxy Server, enable HTTP 1.1. There are several ways to enable HTTP 1.1 through proxy connections:

- In Internet Explorer, go to the **Tools** menu and select **Internet Options**. In the **Advanced** tab, check **Use HTTP 1.1** and **Use HTTP 1.1 through proxy connections**. By default, these are enabled.

   These settings update the **EnableHttp1_1** and **ProxyHttp1.1** values with a DWORD value of one (1) in the following registry key:

   ```
   HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings
   ```
   > [!TIP]
   > The **ProxyHttp1.1** value is not listed in the registry until the value is modified from its default value; which is enabled. If **ProxyHttp1.1** is not listed in this registry key **andUse HTTP 1.1 through proxy connections** is checked in the Internet Explorer settings, then **ProxyHttp1.1is** enabled.

- Modify the Proxy Server settings to allow HTTP 1.1.

- Create a Group Policy to enable HTTP 1.1 through proxy connections. This policy can then be applied to multiple users.

   When creating the policy, it’s typically applied to the Current User.

### Configure the Firewall
The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] uses [!INCLUDE[sb2](/Token/sb2_md.md)] Relays. For outgoing TCP communication, [!INCLUDE[sb2](/Token/sb2_md.md)] Relays use TCP ports 9350 to 9354. Depending on your firewall settings, you may need to create an Outbound Rule for these TCP ports.

[Hosting Behind a Firewall with the Service Bus](http://msdn.microsoft.com/library/windowsazure/ee706729.aspx) provides [!INCLUDE[sb2](/Token/sb2_md.md)] information for Firewalls and Proxy Servers.

## See Also
[Troubleshoot the BizTalk Adapter Service](/Topic/Troubleshoot_the_BizTalk_Adapter_Service.md)
[Using the BizTalk Adapter Service &#40;BAS&#41;](/Topic/Using_the_BizTalk_Adapter_Service__BAS).md)

