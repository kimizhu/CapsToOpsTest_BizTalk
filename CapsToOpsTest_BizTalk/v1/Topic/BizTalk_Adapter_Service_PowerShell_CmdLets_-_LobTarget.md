---
description: na
keywords: na
pagetitle: BizTalk Adapter Service PowerShell CmdLets - LobTarget
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4c2189-2dd6-49c2-90e4-1a00260b532a
---
# BizTalk Adapter Service PowerShell CmdLets - LobTarget
In [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] installs PowerShell cmdlets to perform common [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] tasks, including:

- Get-LOBTarget

- Remove-LOBTarget

- Set-LOBTarget

- New-LOBTarget

## Get-LOBTarget
Get-LOBTarget returns a list of the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Service. Parameters include:

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-ServerUrl *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server URL is the local Management Service: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br />If -ServerURL is specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for that server are returned. <br /> <br />If -ServerURL is not specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-Path *String* <br /> <br />|Optional <br /> <br />|The path to the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server. Path string options include: <br /> <br /><ul><li>Complete URL Path: http://*MyServer*/BAService/ManagementService/Namespace1/target1 </li><li>Relative sub-path: /namespace1/target1 </li> </ul>If -Path is specified, the specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] at that path is returned. <br /> <br />If -Path is not specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-Export *String* <br /> <br />|Optional <br /> <br />|The folder and file name where the serialized configuration of the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] will be stored. <br /> <br />If -Export is specified, the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] serialized configuration will be written to a file. <br /> <br />|
|-Namespace *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] namespace for the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. <br /> <br />If -Namespace is specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for that namespace are returned. <br /> <br />If -Namespace is not specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for all the namespaces on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-LobRelay *String* <br /> <br />|Optional <br /> <br />|The path to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] that hosts the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. <br /> <br />If -[!INCLUDE[lobrelay](/Token/lobrelay_md.md)] is specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s hosted in that specific [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] are returned. <br /> <br />|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Enter this cmdlet to skip the certificate check. <br /> <br />|
|*CommonParameters* <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. They are not specific to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

### Examples

```
// Returns all the LOB Targets from the default Runtime server:
Get-LOBTarget 

// Returns all the LOB Targets in the “ns1” Service Bus namespace from the default Runtime server:
Get-LOBTarget -namespace ns1

// Returns all the LOB Targets hosted at http://MyServer:8080/BAService:
Get-LOBTarget -ServerURL http://MyServer:8080/BAService

// Returns all the LOB Targets hosted in “myLobRelay” from the default Runtime server:
Get- LOBTarget -LobRelay myLobRelay

// Returns the LOB Targets at “/ns1/target1/targetA” from the default Runtime server:
Get-LOBTarget -path /ns1/target1/targetA
```
Additional examples are available by typing: **get-help get-lobtarget -examples**. **get-help get-lobtarget -full** provides more detailed information on this cmdlet.

## Remove-LOBTarget
Remove-LOBTarget removes a [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Service. Parameters include:

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-Path *String* <br /> <br />|Required <br /> <br />|The path to the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server. Path string options include: <br /> <br /><ul><li>Complete URL Path: http://*MyServer*/BAService/ManagementService/Namespace1/target1 </li><li>Relative sub-path: /namespace1/target1 </li> </ul>If -Path is specified, the specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] at that path is removed. <br /> <br />If -Path is not specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are removed. <br /> <br />|
|-ServerUrl *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server URL is the local Management Service: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br />If -ServerURL is specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for that server are removed. <br /> <br />If -ServerURL is not specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are removed. <br /> <br />|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Enter this cmdlet to skip the certificate check. <br /> <br />|
|*CommonParameters* <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. They are not specific to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

### Examples

```c#
// Removes all the LOB Targets from the default Runtime server:
Remove-LOBTarget

// Removes all the LOB Targets in the “ns1” Service Bus namespace from the default Runtime server:
Remove -LOBTarget -namespace ns1

// Removes all the LOB Targets hosted at http://MyServer:8080/BAService:
Remove -LOBTarget –ServerURL http://MyServer:8080/BAService

// Removes the relay path from the default Runtime server:
Remove -LOBTarget -path /relay1
```
Additional examples are available by typing: **get-help remove-lobtarget -examples**. **get-help remove-lobtarget -full** provides more detailed information on this cmdlet.

## Set-LOBTarget
Set-LOBTarget changes an existing [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Service. Parameters include:

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-LobServerUrl *String* <br /> <br />|Optional <br /> <br />|The LOB Server URL to the LOB system. <br /> <br />If -LobServerUrl is specified, update the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to use the specified LOB Server URL. <br /> <br />|
|-UserName *String* <br /> <br />|Optional <br /> <br />|The user name to connect to the LOB system. <br /> <br />If -UserName is specified, updates the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to use the specified LOB user name. <br /> <br />|
|-Password *String* <br /> <br />|Optional <br /> <br />|The user name password to connect to the LOB system. <br /> <br />If -Password is specified, updates the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to use the specified Password. <br /> <br />|
|-Domain *String* <br /> <br />|Optional <br /> <br />|When the LobSecurityType cmdlet is set to **ConfiguredWindowsCredential**, enter the domain name if using a domain account. <br /> <br />If -Domain is specified, updates the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to use the specified domain for the user account. <br /> <br />|
|-LobSecurityType *String* <br /> <br />|Optional <br /> <br />|The security method used to connect to the LOB system. Options include: <br /> <br /><ul><li>CustomSoapHeader </li><li>ConfigureUsername </li><li>ConfiguredWindowsCredential, if using the [!INCLUDE[ssNoVersion](/Token/ssNoVersion_md.md)] LOB system. </li> </ul>If -LobSecurityType is specified, updates the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to use the specified security type. <br /> <br />|
|-HeaderNamespace *String* <br /> <br />|Optional <br /> <br />|The namespace of the username header and the password header. <br /> <br />If -HeaderNamespace is specified, updates the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to use the specified header namespace. <br /> <br />|
|-UserNameHeader *String* <br /> <br />|Optional <br /> <br />|The username header. <br /> <br />If -UserNameHeader is specified, updates the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to use the specified username header. <br /> <br />|
|-PasswordHeader *String* <br /> <br />|Optional <br /> <br />|The password header. <br /> <br />If -PasswordHeader is specified, updates the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to use the specified password header. <br /> <br />|
|-Enable *Boolean* <br /> <br />|Optional <br /> <br />|Specifies to enable or disable the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. Options include: <br /> <br /><ul><li>True: Enables the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] </li><li>False: Disabled the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] </li> </ul>If -Enable is specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are updated. <br /> <br />|
|-ServerUrl *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server URL is the local Management Service: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br />If -ServerURL is specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for that server are updated. <br /> <br />If -ServerURL is not specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s for the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are updated. <br /> <br />|
|-Path *String* <br /> <br />|Required <br /> <br />|The path to the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server. Path string options include: <br /> <br /><ul><li>Complete URL Path: http://*MyServer*/BAService/ManagementService/Namespace1/target1 </li><li>Relative sub-path: /namespace1/target1 </li> </ul>If -Path is specified, the specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] at that path is updated. <br /> <br />If -Path is not specified, all the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are updated. <br /> <br />|
|-InputObject *[!INCLUDE[lobtarget](/Token/lobtarget_md.md)]* <br /> <br />|Required <br /> <br />|Specifies one or more [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to update. This value is specified in the input pipeline. <br /> <br />If -InputObject is specified, that specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is updated. <br /> <br />|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Enter this cmdlet to skip the certificate check. <br /> <br />|
|*CommonParameters* <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. They are not specific to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

### Examples

```c#
// Updates all LOB Targets to use the MyUser account and the MyPassword password:
Set-LOBTarget -LOBUserName MyUser -LOBPassword MyPassword

// Enables all the LOB Targets:
Set-LOBTarget -Enable True

// Updates all the LOB Targets to use the http://MyServer:8080/BAService Runtime server URL:
Set-LOBTarget -ServerURL http://MyServer:8080/BAService

// Updates the LOB Target path to /relay1:
Set -LOBTarget -path /relay1
```
Additional examples are available by typing: **get-help set-lobtarget -examples**. **get-help set-lobtarget -full** provides more detailed information on this cmdlet.

## New-LOBTarget
New-LOBTarget creates a [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Service. Parameters include:

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-RelayPath *String* <br /> <br />|Optional <br /> <br />|Specifies the relay path to be used by the new [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]. The [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] will be created under the relay specified. <br /> <br />If -RelayPath is specified, the new [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] will be created under the relay specified. <br /> <br />|
|-ServerURL *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server URL is the local Management Service: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br />If -ServerURL is specified, the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] for that server is created. <br /> <br />If -ServerURL is not specified, the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created using the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. <br /> <br />|
|-Import *String* <br /> <br />|Required <br /> <br />|Specifies a file name that contains serialized [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] configuration that has already been exported. A [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] can be exported in Server Explorer or by using the **Get-[!INCLUDE[lobtarget](/Token/lobtarget_md.md)] -Path &#42;String&#42; -Export &#42;String&#42;** cmdlet. <br /> <br />If -Import is specified, the [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] configuration will be imported. <br /> <br />|
|-InputObject *LobTarget* <br /> <br />|Rquired <br /> <br />|Specifies one or more [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s to create. This value is specified in the input pipeline. <br /> <br />If -InputObject is specified, that specific [!INCLUDE[lobtarget](/Token/lobtarget_md.md)] is created. <br /> <br />|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Enter this cmdlet to skip the certificate check. <br /> <br />|
|*CommonParameters* <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. They are not specific to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

### Examples

```
// Creates a new LOB Target from the MyFile serialized configuration in the default Runtime server:
New-LOBTarget -Import MyFile

// Creates a new LOB Target hosted at http://MyServer:8080/BAService:
New -LOBTarget -ServerURL http://MyServer:8080/BAService

// Creates a new LOB Target in the specified /relay1 relay path in the default Runtime server:
New -LOBTarget -RelayPath /relay1
```
Additional examples are available by typing: **get-help new-lobtarget -examples**. **get-help new-lobtarget -full** provides more detailed information on this cmdlet.

## See Also
[BizTalk Adapter Service PowerShell CmdLets - LobRelay](/Topic/BizTalk_Adapter_Service_PowerShell_CmdLets_-_LobRelay.md)
[PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md)
[LOB Security in BizTalk Adapter Service](/Topic/LOB_Security_in_BizTalk_Adapter_Service.md)
[about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkId=113216)

