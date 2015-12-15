---
description: na
keywords: na
pagetitle: Troubleshoot the BizTalk Adapter Service
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cb23b29-7446-45ce-952f-a5263dcb5777
---
# Troubleshoot the BizTalk Adapter Service
Enable tracing and performance counters in the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)].

The **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime** and **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management** components use the .Net Framework System.Diagnostics trace source and the XML Trace Listener. In a [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Application, tracing events can be enabled for the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime** and **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management** components.

### To enable runtime tracing

1. Go to the Microsoft [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime folder. By default, the folder is *C:\Program Files\Microsoft [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]\BAServiceRuntime*.

2. Open the **web.config** file in Notepad.

3. In the **&lt;configuration&gt;** node, add the following **&lt;system.diagnostics&gt;** section:

   ```
   <system.diagnostics>
      <sources>
         <source name="Microsoft.ApplicationServer.Integration.BAService.Runtime" switchValue="Information">
            <listeners>
            <add name="BAServiceRuntimeTrace" />
            </listeners>
         </source>
      </sources>
      <trace autoflush="true" />
      <sharedListeners>
         <add name="BAServiceRuntimeTrace" type="System.Diagnostics.XmlWriterTraceListener" initializeData="c:\temp\RuntimeTraceFile.xml" />
      </sharedListeners>
   </system.diagnostics>
   ```
   > [!IMPORTANT]
   > The trace file name and location can be any name and path you prefer. In the &lt;sharedListeners&gt; section above, RuntimeTraceFile.xml is the trace file name and is created in the c:\temp folder.

4. Within the **&lt;system.servicemodel&gt;** node inside the web.config, add the following **&lt;diagnostics&gt;** section:

   ```
   <diagnostics>
     <messageLogging
       logEntireMessage="true"
       logMalformedMessages="true"
       logMessagesAtServiceLevel="true"
       logMessagesAtTransportLevel="true"
       maxMessagesToLog="3000"
       maxSizeOfMessageToLog="2000"/>
   </diagnostics>
   ```

5. Save changes to the web.config.

### To enable management tracing

1. Go to the Microsoft [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management folder. By default, the folder is *C:\Program Files\Microsoft [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]\BAService*.

2. Open the web.config file in Notepad.

3. In the **&lt;configuration&gt;** section, add the following **&lt;system.diagnostics&gt;** section:

   ```
   <system.diagnostics>
      <sources>
         <source name="Microsoft.ApplicationServer.Integration.BAService.Management" switchValue="Information">
            <listeners>
            <add name="BAServiceManagementTrace" />
            </listeners>
         </source>
      </sources>
      <trace autoflush="true" />
      <sharedListeners>
         <add name="BAServiceManagementTrace" type="System.Diagnostics.XmlWriterTraceListener" initializeData="c:\temp\ManagementTraceFile.xml" />
      </sharedListeners>
   </system.diagnostics>
   ```
   > [!IMPORTANT]
   > The trace file name and location can be any name and path you prefer. In the &lt;sharedListeners&gt; section above, ManagementTraceFile.xml is the trace file name and i created in the c:\temp folder.

4. Within the **&lt;system.servicemodel&gt;** node inside the web.config, add the following **&lt;diagnostics&gt;** section:

   ```
   <diagnostics>
     <messageLogging
       logEntireMessage="true"
       logMalformedMessages="true"
       logMessagesAtServiceLevel="true"
       logMessagesAtTransportLevel="true"
       maxMessagesToLog="3000"
       maxSizeOfMessageToLog="2000"/>
   </diagnostics>
   ```

5. Save changes to the web.config.

## Supported switchValue options
[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] supports the following **switchValue** options:

- Off

- Critical

- Error

- Warning

- Information

- Verbose

- ActivityTracing

- All

[Configuring Tracing](http://go.microsoft.com/fwlink/p/?LinkId=193433) lists the tracked events of the different Tracing levels.

## To enable Performance Monitor counters
The **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime** and **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management** components utilize Performance Monitor. By default, these performance counters are enabled.

1. To enable or disable the Management performance counters:

   1. In IIS, expand **Sites**, and expand **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**.

   2. Select the **BAService** application and select **Application Settings**.

   3. To enable the performance counters, set **EnablePerfCounter** to True. To disable the performance counters, set **EnablePerfCounter** to False.

   Performance counters can also be enabled in the web.config file (*\Program Files\Microsoft [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]\BAService*):

   ```
   <appSettings>
       <add key="EnablePerfCounters" value="True" />
   </appSettings>
   ```
   When enabled, the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Management** object is available in Performance Monitor with the following counters:

   - AverageTimeToCreateRelay

   - AverageTimeToCreateTarget

   - AverageTimeToDeleteRelay

   - AverageTimeToDeleteTarget

   - AverageTimeToUpdateRelay

   - AverageTimeToUpdateTarget

2. To enable or disable the Runtime performance counters:

   1. In IIS, expand **Sites** and expand **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]**.

   2. Select the application that corresponds to the relay and select **Application Settings**.

   3. To enable the performance counters, set **EnablePerfCounter** to True. To disable the performance counters, set **EnablePerfCounter** to False.

   Performance counters can also be enabled in the web.config file (*\Program Files\Microsoft [!INCLUDE[lobconnect](/Token/lobconnect_md.md)]\BAServiceRuntime*):

   ```
   <appSettings>
       <add key="EnablePerfCounters" value="True" />
       <add key="ReConnectIntervalInSeconds" value="30" />
   </appSettings>
   ```
   When enabled, the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime** object is available in Performance Monitor with the following counters:

   - AverageTimeToOpenChannel

   - AverageTimeToSend

## Runtime URL: Unable to connect
During the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] installation, you choose whether to allow SSL connections. The Runtime URL automatically defaults to HTTP or HTTPS depending on your SSL choice. In some scenarios, you may be unable to connect to the Runtime URL.

In the following scenarios, you may need to change from the default HTTP/HTTPS setting:

- You installed the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] with the no SSL option. From another computer, you connect to the Runtime URL. In this scenario, you must enter HTTP for the Runtime URL:

   http://*ServerName*:8080/BAService/ManagementService.svc/

- You installed the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] locally and allowed SSL connections. You reinstall the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] and don’t allow SSL connections. In this scenario, you must enter HTTP for the Runtime URL:

   http://localhost:8080/BAService/ManagementService.svc/

## See Also
[Troubleshoot Azure BizTalk Services](/Topic/Troubleshoot_Azure_BizTalk_Services.md)
[Windows Performance Monitor](http://go.microsoft.com/fwlink/p/?LinkID=132016)

