---
description: na
keywords: na
pagetitle: BizTalk Adapter Service PowerShell CmdLets - LobRelay
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0bd0f932-40ff-4fcf-952e-a65a8137ecd8
---
# BizTalk Adapter Service PowerShell CmdLets - LobRelay
In [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)], [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] installs PowerShell cmdlets to perform common [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] tasks, including:

- Get-LOBRelay

- New-LOBRelay

- Remove-LOBRelay

- Set-LOBRelay

## Get-LOBRelay
Get-LOBRelay returns a list of the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime. Parameters include:

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-ServerUrl *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server URL is the local Management Service: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br />If -ServerURL is specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for that server are returned. <br /> <br />If -ServerURL is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-Path *String* <br /> <br />|Optional <br /> <br />|The path to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server. Path string options include: <br /> <br /><ul><li>Complete URL Path: http://*MyServer*/BAService/ManagementService/Namespace1/relay1 </li><li>Relative sub-path: /namespace1/relay1 </li> </ul>If -Path is specified, the specific [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] at that path is returned. <br /> <br />If -Path is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-Namespace *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] namespace for the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s. <br /> <br />If -Namespace is specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for that namespace are returned. <br /> <br />If -Namespace is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for all the namespaces on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Enter this cmdlet to skip the certificate check. <br /> <br />|
|*CommonParameters* <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. They are not specific to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

### Examples

```
// Returns all the LOB Relays from the default Runtime server:
Get-LOBRelay 

// Returns all the LOB Relays in the ns1 Service Bus namespace from the default Runtime server:
Get-LOBRelay -namespace ns1

// Returns all the LobRelays hosted at http://MyServer:8080/BAService:
Get-LOBRelay –ServerURL http://MyServer:8080/BAService

// Returns the relay path from the default Runtime server:
Get-LOBRelay -path /relay1
```
Additional examples are available by typing: **get-help Get-LOBRelay -examples**. **get-help get-lobrelay -full** provides more detailed information on this cmdlet.

## New-LOBRelay
Creates a new [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime. Parameters include:

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-RelayPath *String* <br /> <br />|Required <br /> <br />|The path to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server. RelayPath string options include: <br /> <br /><ul><li>Complete URL Path: http://*MyServer*/BAService/ManagementService/Namespace1/relay1 </li><li>Relative sub-path: /namespace1/relay1 </li> </ul>If -RelayPath is specified, the specific [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] at that path is returned. <br /> <br />If -RelayPath is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-Namespace *String* <br /> <br />|Required <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] namespace for the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s. <br /> <br />If -Namespace is specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for that namespace are returned. <br /> <br />If -Namespace is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for all the namespaces on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-IssuerName *String* <br /> <br />|Required <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name. <br /> <br />If -IssuerName is specified, the -IssuerSecret must also be specified. <br /> <br />|
|-IssuerSecret *String* <br /> <br />|Required <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Secret key. <br /> <br />If -IssuerSecret is specified, -IssuerName must also be specified. <br /> <br />|
|-Status *RelayStatus* <br /> <br />|Optional <br /> <br />|Starts or stops a [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. Options include: <br /> <br /><ul><li>Stopped </li><li>Started </li> </ul>If -Status is specified, all [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s are updated with the specified status. <br /> <br />|
|-UseMessageCredentials *Boolean* <br /> <br />|Optional <br /> <br />|Default is False. When set to False, the logon credentials are NOT included in the WS-Security header of the message. When to set to True, the logon credentials are included in the WS-Security header of the message. <br /> <br />|
|-ServerUrl *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server URL is the local Management Service: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br />If -ServerURL is specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for that server are returned. <br /> <br />If -ServerURL is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are returned. <br /> <br />|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Enter this cmdlet to skip the certificate check. <br /> <br />|
|*CommonParameters* <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. They are not specific to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

### Examples

```
// Creates a new LOBRelay using MyNamespace, MyIssuerKey, and MyIssuerName on the default Runtime server:
New-LOBRelay –Namespace MyNamespace -IssuerSecret MyIssuerKey -IssuerName MyIssuerName

// Creates a new LOBRelay in the stopped state on the default Runtime server:
New-LOBRelay –Namespace MyNamespace –IssuerName MyIssuerName –IssuerSecret MyIssuerKey -Status stopped

// Creates a new LOBRelay using Message Security hosted at http://MyServer:8080/BAService:
New-LOBRelay –Namespace -IssuerSecret MyIssuerKey -IssuerName MyIssuerName –UseMessageCredentials True -ServerURL http://MyServer:8080/BAService

// Creates a new LOBRelay using the “relay1” path in a started state on the default Runtime server and skipping the certificate validation:
New-LOBRelay New-LOBRelay –Namespace -IssuerSecret MyIssuerKey -IssuerName MyIssuerName -relaypath /relay1 -Status started -SkipCertCheck
```
Additional examples are available by typing: **get-help New-LOBRelay -examples**. **get-help new-lobrelay -full** provides more detailed information on this cmdlet.

## Remove-LOBRelay
Removes a [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime. Parameters include:

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-ForceDelete <br /> <br />|Optional <br /> <br />|Deletes a [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] even if it contains [!INCLUDE[lobtarget](/Token/lobtarget_md.md)]s. <br /> <br />|
|-Path *String* <br /> <br />|Required <br /> <br />|The path to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server. Path string options include: <br /> <br /><ul><li>Complete URL Path: http://*MyServer*/BAService/ManagementService/Namespace1/relay1 </li><li>Relative sub-path: /namespace1/relay1 </li> </ul>If -Path is specified, the specific [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] at that path is removed. <br /> <br />If -Path is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are removed. <br /> <br />|
|-ServerUrl *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server URL is the local Management Service: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br />If -ServerURL is specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for that server are removed. <br /> <br />If -ServerURL is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are removed. <br /> <br />|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Enter this cmdlet to skip the certificate check. <br /> <br />|
|*CommonParameters* <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. They are not specific to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

### Examples

```
// Removes all the LOBRelays from the default Runtime server:
Remove-LOBRelay 

// Removes all LOBRelays from the default Runtime server, even if the LOBRelay has LOBTargets:
Remove-LOBRelay -ForceDelete

// Removes all the LOBRelays in the ns1 Service Bus namespace from the default Runtime server:
Remove -LOBRelay -namespace ns1

// Removes all the LOBRelays hosted at http://MyServer:8080/BAService:
Remove -LOBRelay -ServerURL http://MyServer:8080/BAService

// Removes the “relay1” relay path from the default Runtime server:
Remove -LOBRelay -path /relay1
```
Additional examples are available by typing: **get-help Remove-LOBRelay -examples**. **get-help remove-lobrelay -full** provides more detailed information on this cmdlet.

## Set-LOBRelay
Set-LOBRelay updates an existing [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime. Parameters include:

|Parameter <br /> <br />|Requirement <br /> <br />|Description <br /> <br />|
|-------------|---------------|---------------|
|-IssuerName *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Name. <br /> <br />If -IssuerName is specified, the -IssuerSecret must also be specified. <br /> <br />|
|-IssuerSecret *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[sb2](/Token/sb2_md.md)] Issuer Secret key. <br /> <br />If -IssuerSecret is specified, -IssuerName must also be specified. <br /> <br />|
|-Status *RelayStatus* <br /> <br />|Optional <br /> <br />|Starts or stops a [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]. Options include: <br /> <br /><ul><li>Stopped </li><li>Started </li> </ul>If -Status is specified, all [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s are updated with the specified status. <br /> <br />|
|-Path *String* <br /> <br />|Required <br /> <br />|The path to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] on the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime Server. Path string options include: <br /> <br /><ul><li>Complete URL Path: http://*MyServer*/BAService/ManagementService/Namespace1/relay1 </li><li>Relative sub-path: /namespace1/relay1 </li> </ul>If -Path is specified, the specific [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] at that path is updated. <br /> <br />If -Path is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s on the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are updated. <br /> <br />|
|-ServerUrl *String* <br /> <br />|Optional <br /> <br />|The [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime URL of the [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server. The default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server URL is the local Management Service: <br /> <br />http://localhost:8080/BAService/ManagementService/ <br /> <br />or <br /> <br />https://localhost:8080/BAService/ManagementService/ <br /> <br />If -ServerURL is specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for that server are updated. <br /> <br />If -ServerURL is not specified, all the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s for the default [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] Runtime server are updated. <br /> <br />|
|-SkipCertCheck <br /> <br />|Optional <br /> <br />|Enter this cmdlet to skip the certificate check. <br /> <br />|
|-InputObject *[!INCLUDE[lobrelay](/Token/lobrelay_md.md)]* <br /> <br />|Required <br /> <br />|Specifies one or more [!INCLUDE[lobrelay](/Token/lobrelay_md.md)]s to update. This value is specified in the input pipeline. <br /> <br />If -InputObject is specified, that specific [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] is updated. <br /> <br />|
|[*CommonParameters*] <br /> <br />|Optional <br /> <br />|Can be used with any cmdlet and are implemented by Windows PowerShell. They are not specific to [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] PowerShell. Options include: <br /> <br /><ul><li>-Verbose </li><li>-Debug </li><li>-ErrorActions </li><li>-ErrorVariable </li><li>-WarningAction </li><li>-WarningVariable </li><li>-OutBuffer </li><li>-OutVariable </li> </ul>**get-help about_commonparameters** provides detailed information about these common parameters. [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkId=113216) is also a good resource. <br /> <br />|

### Examples

```
// Updates all LOBRelays to a stopped state on the default Runtime server:
Set-LOBRelay -Status stopped

// Updates all the LOBRelays to use MySecretKey and MySecretName in the default Runtime server:
Set-LOBRelay -IssuerSecret MySecretKey -IssuerName MySecretName

// Updates all the LOBRelays to a started state hosted at http://MyServer:8080/BAService:
Set-LOBRelay -ServerURL http://MyServer:8080/BAService -Status started

// Updates the “relay1” relay path to a stopped state from the default Runtime server:
Set-LOBRelay -path /relay1 -Status stopped
```
Additional examples are available by typing: **get-help Set-LOBRelay -examples**. **get-help set-lobrelay -full** provides more detailed information on this cmdlet.

## See Also
[BizTalk Adapter Service PowerShell CmdLets - LobTarget](/Topic/BizTalk_Adapter_Service_PowerShell_CmdLets_-_LobTarget.md)
[PowerShell Cmdlets for the BizTalk Adapter Service](/Topic/PowerShell_Cmdlets_for_the_BizTalk_Adapter_Service.md)
[LOB Security in BizTalk Adapter Service](/Topic/LOB_Security_in_BizTalk_Adapter_Service.md)
[Windows PowerShell Cmdlet Help Topics](http://go.microsoft.com/fwlink/p/?LinkId=113277)
[about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkId=113216)

