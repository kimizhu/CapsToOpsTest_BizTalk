---
description: na
keywords: na
pagetitle: Release Notes for Azure BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8fb45528-57eb-45ba-886b-6513da2fe296
---
# Release Notes for Azure BizTalk Services
The release notes for the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] contain the known issues in this release.

## What’s new in the November update of BizTalk Services
Encryption at Rest can be enabled in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. See [Enable Encryption at Rest in BizTalk Services Portal](/Topic/Enable_Encryption_at_Rest_in_BizTalk_Services_Portal.md).

## Update History

|Update <br /> <br />|Changes <br /> <br />|
|----------|-----------|
|**October Update** <br /> <br />|<ul><li>Organizational accounts are supported: <br /> <br /><ul><li>**Scenario**: You registered a BizTalk Service deployment using a Microsoft account (like user@live.com). In this scenario, only Microsoft Account users can manage the BizTalk Service using the BizTalk Services portal. An organizational account cannot be used. </li><li>**Scenario**: You registered a BizTalk Service deployment using an organizational account in an Azure Active Directory (like  user@fabrikam.com or user@contoso.com). In this scenario, only Azure Active Directory users within the same organization can manage the BizTalk Service using the BizTalk Services portal. A Microsoft account cannot be used. </li> </ul> </li><li>When you create a BizTalk Service in the [!INCLUDE[azportal](/Token/azportal_md.md)], you are automatically registered in the [!INCLUDE[af_integration](/Token/af_integration_md.md)] Portal. <br /> <br />   **Scenario**: You log into the [!INCLUDE[azportal](/Token/azportal_md.md)], create a BizTalk Service, and then select **Manage** for the very first time. When the [!INCLUDE[af_integration](/Token/af_integration_md.md)] portal opens, the BizTalk Service automatically registers and is ready for your deployments. </li> </ul>See [Registering and Updating a BizTalk Service Deployment on the BizTalk Services Portal](/Topic/Registering_and_Updating_a_BizTalk_Service_Deployment_on_the_BizTalk_Services_Portal.md). <br /> <br />|
|**August 14 Update** <br /> <br />|<ul><li>Agreement and bridge decoupling – Trading partner agreements and bridges are now decoupled in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. You now create agreements and bridges separately, and at runtime bridges resolve to an agreement based on the values in the EDI message. See [Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md), [Create an EDI bridge using BizTalk Services Portal](/Topic/Create_an_EDI_bridge_using_BizTalk_Services_Portal.md), [Create an AS2 bridge using BizTalk Services Portal](/Topic/Create_an_AS2_bridge_using_BizTalk_Services_Portal.md), and [How do bridges resolve agreements at runtime?](/Topic/How_do_bridges_resolve_agreements_at_runtime_.md) </li><li>The option to create templates for agreements is discontinued. </li><li>For the send-side agreement, you can now specify different delimiter sets for each schema. This configuration is specified under protocol settings for send side agreement. For more information, see [Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md) and [Create an EDIFACT Agreement in Azure BizTalk Services](/Topic/Create_an_EDIFACT_Agreement_in_Azure_BizTalk_Services.md). Two new entities are also added to the TPM OM API for the same purpose. See [X12DelimiterOverrides](/Topic/X12DelimiterOverrides.md) and [EDIFACTDelimiterOverride](/Topic/EDIFACTDelimiterOverride.md). </li><li>Standard XSD constructs, including Derived Types, are now supported. See [Use standard XSD constructs in your maps](/Topic/Use_standard_XSD_constructs_in_your_maps.md) and [Use Derived Types in Mapping Scenarios and Examples](/Topic/Use_Derived_Types_in_Mapping_Scenarios_and_Examples.md). </li><li>AS2 supports new MIC algorithms for message signing and new encryption algorithms. See [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md). </li> </ul>|

## <a name="BKMK_KnownIssues"></a>Known Issues
The following section lists known issues in this release of the [!INCLUDE[af_integration](/Token/af_integration_md.md)]:

### Connectivity Issues after BizTalk Services Portal Update
If you have the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] open while [!INCLUDE[af_integration](/Token/af_integration_md.md)] is upgraded to roll in changes to the service, you might face connectivity issues with the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

As a workaround, you may restart the browser, delete the browser cache, or start the portal in private mode.

### Visual Studio IDE cannot locate the artifact if you click an error or warning in a BizTalk Services project
Install the [Visual Studio 2012 Update 3 RC 1](http://go.microsoft.com/fwlink/p/?LinkId=304174) to fix the issue.

### Custom binding project reference
Consider the following situations with a [!INCLUDE[af_integration](/Token/af_integration_md.md)] project in a [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] solution:

- In the same [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] solution, there is a [!INCLUDE[af_integration](/Token/af_integration_md.md)] project **and** a custom binding project. The [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] has a reference to this custom binding project file.

- The [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] has a reference to a custom binding/behavior DLL.

You ‘Build’ the solution in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)] successfully. Then, you ‘Rebuild’ or ‘Clean’ the solution. After that, when you rebuild or clean again, the following error occurs:

```
Unable to copy file <Path to DLL> to “bin\Debug\FileName.dll”. The process cannot access the file ‘bin\Debug\FileName.dll’ because it is being used by another process.
```
**Workaround**

- If [Visual Studio 2012 Update 3](http://www.microsoft.com/download/details.aspx?id=39305) is installed, you have the following two options:

   - Restart [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)], or

   - Restart the solution. Then, perform only a Build on the solution.

- If [Visual Studio 2012 Update 3](http://www.microsoft.com/download/details.aspx?id=39305) is **not** installed, open Task Manager, click the **Processes** tab, click the MSBuild.exe process, and then click the **End Process** button.

### Routing to BasicHttpRelay endpoints is not supported from [!INCLUDE[bridge](/Token/bridge_md.md)]s and [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] if non-printable characters are promoted as HTTP headers
If you use non-printable characters as part of promoted properties for messages, those messages cannot be routed to relay destinations that use the BasicHttpRelay binding. Also, the promoted properties that are available as part of tracking are URL-encoded for blobs and un-encoded for destinations.

### MDN is sent asynchronously even if the Send asynchronous MDN option is unchecked
Consider this scenario – If you select the **Send asynchronous MDN** checkbox and, specify a URL to send the async MDN to, and then uncheck the **Send asynchronous MDN** checkbox again, the MDN is still sent to the specified URL even though the option to send async MDNs is not selected.

As a workaround, you must clear the specified URL before unchecking the **Send asynchronous MDN** checkbox and then deploy the AS2 agreement.

### Whitespace characters beyond a valid interchange cause an empty message to be sent to the suspend endpoint
If there are whitespaces beyond an IEA segment, the disassembler treats this as end of current interchange and looks at the next set of whitespaces as a next message. Since this is not valid interchange, you might observe that one successful message is sent to the route destination and one empty message is sent the suspend endpoint.

### Tracking in BizTalk Services Portal
Tracking events are captured up to the EDI message processing and any correlation. If a message fails outside of the Protocol stage, Tracking will show as successful. In this situation, refer to the LOG section under the **Details** column in **Tracking** for error details.

The X12 Receive and Send settings ([Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md)) provide information on the Protocol stage.

### Update Agreement
The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] allows you to modify the Qualifier of an Identity when an agreement is configured. This can result in inconsistence properties. For example, there is an agreement using ZZ:1234567 and ZZ:7654321 the Qualifier. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] profile settings, you change ZZ:1234567 to be 01:*ChangedValue*. You open the agreement and 01:*ChangedValue* is displayed instead of ZZ:1234567.

To modify the Qualifier of an identity, delete the agreement, update **Identities** in the partner profile and then recreate the agreement.

> [!WARNING]
> This behavior impacts X12 and AS2.

### AS2 Attachments
Attachments for AS2 messages are not supported in send or receive. Specifically, attachments are silently ignored and the message body is processed as a regular AS2 message.

### Resources: Remembering Path
When adding **Resources**, the dialog window may not remember the path previously used to add a resource. To remember the previously-used path, try adding the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] web site to **Trusted Sites** in Internet Explorer.

### If you rename the entity name of a bridge and close the project without saving changes, opening the entity again results in an error
Consider a scenario in the following order:

- Add a [!INCLUDE[bridge](/Token/bridge_md.md)] (for example an [!INCLUDE[one-way](/Token/one-way_md.md)]) to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]

- Rename the [!INCLUDE[bridge](/Token/bridge_md.md)] by specifying a value for the **Entity Name** property. This renames the associated .bridgeconfig file with the name you specified.

- Close the .bcs file (by closing the tab in Visual Studio) without saving the changes.

- Open the .bcs file again from the Solution Explorer.

   You will notice that while the associated .bridgeconfig file has the new name you specified, the entity name on the design surface is still the old name. If you try to open the [!INCLUDE[msgflow](/Token/msgflow_md.md)] by double-clicking the bridge component, you get the following error:

   ```
   ‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist
   ```

To avoid running into this scenario, make sure you save changes after you rename the entities in a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)].

### [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] builds successfully even if an artifact has been excluded from a Visual Studio project
Consider a scenario where you add an artifact (for example, an XSD file) to a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], include that artifact in the [!INCLUDE[msgflow](/Token/msgflow_md.md)] (for example, by specifying it as a Request message type), and then exclude it from the Visual Studio project. In such a case, building the project will not give any error as long as the deleted artifact is available on the disk at the same location from where it was included in the Visual Studio project.

### The [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] does not check for schema availability while configuring the bridges
In a [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], if a schema that is added to the project imports another schema, the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] does not check whether the imported schema is added to the project. If you try to build such a project, you do not get any build errors.

### The response message for a [!INCLUDE[request_response](/Token/request_response_md.md)] is always of charset UTF-8
For this release, the charset of the response message from an [!INCLUDE[request_response](/Token/request_response_md.md)] is always set to UTF-8.

### User-Defined Datatypes
The [!INCLUDE[bap](/Token/bap_md.md)] adapters within the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] feature can utilize user-defined datatypes for adapter operations.

When using user-defined datatypes, copy the files (.dll) to *drive*:\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime\bin\ **or** to the Global Assembly Cache (GAC) on the server hosting the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] service. Otherwise, the following error may occur on the client:

```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <faultcode>s:Client</faultcode>
  <faultstring xml:lang="en-US">The UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing the assembly containing the UDT definition in the Global Assembly Cache.</faultstring>
  <detail>
    <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
    </AFConnectRuntimeFault>
  </detail>
</s:Fault>
```
> [!IMPORTANT]
> It is recommended to use GACUtil.exe to install a file into the Global Assembly Cache. [GACUtil.exe](http://go.microsoft.com/fwlink/p/?LinkID=169103) documents how to use this tool and the Visual Studio command line options.

### Restarting the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Web Site
Installing the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime** creates the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site in IIS that contains the **BAService** application. **BAService** application internally uses relay binding to extend the reach of on-premise service endpoint to the cloud. For a service hosted on-premises, the corresponding relay endpoint will be registered on the Service Bus only when the on-premises service starts.

If you stop and start an application, the configuration for auto-starting an application is not honored. So when **BAService** is stopped, you must always restart the **[!INCLUDE[lobconnect](/Token/lobconnect_md.md)]** web site instead. Do **not** start or stop the **BAService** application.

### Special characters should not be used for address and entity names of LOB components
You should not use special characters for address and entity names of LOB components. If you do so, you will get an error while deploying the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. For certain characters like ‘%’, the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] website might go into a stopped state and you will have to manually start it.

### Test Map with Get Context Property
If a [!INCLUDE[transform](/Token/transform_md.md)] contains a **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)], **Test Map** will fail. As a temporary workaround, replace the **Get Context Property**[!INCLUDE[mapop](/Token/mapop_md.md)] with a String Concatenate [!INCLUDE[mapop](/Token/mapop_md.md)] containing dummy data. This will populate the target schema and allow you test other Transform functionality.

### Test Map Property does not display
The **Test Map** properties do not display in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)]. This can occur if the **Properties** window **and** the **Solution Explorer** window are not simultaneously docked. To resolve this, dock the **Propertiesand** the **Solution Explorer** windows.

### DateTime Reformat drop-down is grayed out
When a DateTime Reformat [!INCLUDE[mapop](/Token/mapop_md.md)] is added to the design surface and configured, the Format drop-down list may be grayed out. This can happen if the computer Display is set **Medium – 125%** or **Larger – 150%**. To resolve, set the display to **Smaller – 100% (default)** using the steps below:

1. Open the **Control Panel** and click **Appearance and Personalization**.

2. Click **Display**.

3. Click **Smaller – 100% (default)** and click **Apply**.

The **Format** drop-down list should now work as expected.

### Duplicate agreements in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]
Consider the following scenario:

1. Create an agreement using the Trading Partner Management OM API.

2. Open the agreement in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] in two different tabs.

3. Deploy the agreement from both the tabs.

4. As a result, both the agreements get deployed resulting in duplicate entries in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]

**Workaround**. Open any one of the duplicate agreements in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], and undeploy.

### Bridges do not use updated certificate even after a certificate has been updated in the artifact store
Consider the following scenarios:

**Scenario 1: Using thumbprint-based certificates for securing message transfer from a bridge to a service endpoint**

Consider a scenario where you use thumbprint-based certificates in your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. You update the certificate in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] with the same name but a different thumbprint, but do not update the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] accordingly. In such a scenario, the bridge might continue to process the messages because the older certificate data might still be in the channel cache. After that, message processing fails.

Workaround: Update the certificate in the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and redeploy the project.

**Scenario 2: Using name-based behaviors to identify certificates for securing message transfer from a bridge to a service endpoint**

Consider a scenario where you use name-based behaviors to identify certificates in your [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. You update the certificate in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] but do not update the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] accordingly.  In such a scenario, the bridge might continue to process the messages because the older certificate data might still be in the channel cache. After that, message processing fails.

Workaround: Update the certificate in the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] and redeploy the project.

### Bridges continue to process messages even when the SQL database is offline
The [!INCLUDE[af_integration](/Token/af_integration_md.md)] bridges continue to process messages for a while, even if the [!INCLUDE[ssSDSfull](/Token/ssSDSfull_md.md)] (which stores the running information like deployed artifacts and pipelines), is offline. This is because [!INCLUDE[af_integration](/Token/af_integration_md.md)] uses the cached artifacts and bridge configuration.

If you do not want the bridges to process any messages when the [!INCLUDE[SQLAzDb](/Token/SQLAzDb_md.md)] is offline, you can use the [!INCLUDE[af_integration](/Token/af_integration_md.md)] PowerShell cmdlets to stop or suspend the BizTalk Service. See [Azure BizTalk Service Management Sample](http://go.microsoft.com/fwlink/p/?LinkID=329019) for the Windows PowerShell cmdlets to manage operations.

### Reading the XML message within a bridge’s custom code component includes an extra BOM character
Consider a scenario where you want to read an XML message within a bridge’s custom code. If you use the .NET API `System.Text.Encoding.UTF8.GetString(bytes)` an extra BOM character is included in the output at the beginning of the message. So, if you do not want the output to include the extra BOM character, you must use `System.IO.StreamReader().ReadToEnd()`.

### Sending messages to a bridge using WCF does not scale
Messages sent to a bridge using WCF does not scale. You should instead use HttpWebRequest if you want a scalable client.

### UPGRADE: Token Provider error after upgrading from BizTalk Services Preview to General Availability (GA)
There is an EDI or AS2 Agreement with active batches. When the BizTalk Service is upgraded from Preview to GA, the following may occur:

- Error: The token provider was unable to provide a security token. Token provider returned message: The remote name could not be resolved.

- Batch tasks are cancelled.

**Workaround**: After the BizTalk Service is updated to General Availability (GA), redeploy the agreement.

### UPGRADE: Toolbox shows the old bridge icons after upgrading the [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK
After you upgrade an earlier version of the [!INCLUDE[af_integration](/Token/af_integration_md.md)] SDK, which had old icons representing the bridges, the toolbox continues to show the old icons for the bridges. However, if you add a bridge to [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] designer surface, the surface shows the new icon.

**Workaround**. You can work around this issue by deleting the .tbd files under `*<system drive>*:\Users\*<user>*\AppData\Local\Microsoft\VisualStudio\11.0`.

### UPGRADE: BizTalk Portal update from Preview to GA might show an error indicating that the EDI capability is not available
If you are logged into the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] while the [!INCLUDE[af_integration](/Token/af_integration_md.md)] is upgraded from Preview to GA, you might get the following error on the portal:

`This capability is not available as part of this edition of [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]. To use these capabilities switch to an appropriate edition.`

**Resolution**: Log out from the portal, close and open the browser, and then log into the portal.

### UPGRADE: New tracking data does not show up after BizTalk Services is upgraded to GA
Assume a scenario where you have an [!INCLUDE[xml_bridge](/Token/xml_bridge_md.md)] deployed on [!INCLUDE[af_integration](/Token/af_integration_md.md)] Preview subscription. You send messages to the bridge and the corresponding tracking data is available on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. Now, if the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] and [!INCLUDE[af_integration](/Token/af_integration_md.md)] runtime bits are upgraded to GA, and you send a message to the same bridge endpoint deployed earlier, the tracking data does not show up for messages sent after upgrade.

### Pipelines v/s Bridges
Throughout this document, the term ‘pipelines’ and ‘bridges’ are used interchangeably. Both essentially mean the same thing, which is, a message processing unit deployed on [!INCLUDE[af_integration](/Token/af_integration_md.md)].

## See Also
[BizTalk Services](/Topic/BizTalk_Services.md)

