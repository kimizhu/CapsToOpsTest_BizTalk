---
description: na
keywords: na
pagetitle: Trading Partner Management Object Model: REST Endpoint
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b4abc6d-2fcb-4e95-830b-938aa3c50f8f
---
# Trading Partner Management Object Model: REST Endpoint
REST endpoint used for the TPM OM APIs.

After you have provisioned your BizTalk Service (steps at [http://go.microsoft.com/fwlink/p/?LinkId=299821](http://go.microsoft.com/fwlink/p/?LinkId=299821)), a deployment URL is created for your environment. You can use that URL to arrive at the REST endpoint used for the TPM OM APIs.

In this topic:

[Discovering the TPM OM Entities](/Topic/Trading_Partner_Management_Object_Model__REST_Endpoint.md#BKIMK_TPMOmEntities)

[TPM OM API: What to do Where?](/Topic/Trading_Partner_Management_Object_Model__REST_Endpoint.md#BKMK_TPMWhatWhere)

[Connecting to the TPM OM API REST Endpoint](/Topic/Trading_Partner_Management_Object_Model__REST_Endpoint.md#BKMK_TPMEndpoint)

[Creating .NET Applications Using the TPM OM API](/Topic/Trading_Partner_Management_Object_Model__REST_Endpoint.md#BKMK_TPMNetApps)

## <a name="BKIMK_TPMOmEntities"></a>Discovering the TPM OM Entities
TPM OM API uses the `$metadata` operation to make the entities discoverable. The URI to retrieve the metadata is:

```
<base_URL>/default/$PartnerManagement/$metadata
```
Here, *&lt;base_URL&gt;* refers to the deployment URL of the [!INCLUDE[af_integration](/Token/af_integration_md.md)] environment. For example, if the deployment URL is `https://mybiztalkservice.biztalk.windows.net`, the URL to retrieve the metadata should be `https://mybiztalkservice.biztalk.windows.net/default/$PartnerManagement/$metadata`.

This URL allows you to retrieve all valid entity types, entity properties, associations, and so on. You can also view the metadata by hitting the endpoint in a browser.

## <a name="BKMK_TPMWhatWhere"></a>TPM OM API: What to do Where?
The TPM OM API enables users to write applications to create and manage the entities required in business-to-business messaging. While the object model aims to have complete parity with the operations available through the portal, there are some tasks that are done outside the use of the object model. This section provides information on the tasks that can be performed using the object model, the tasks that can be performed using the [PowerShell CmdLets to manage the BizTalk Service](/Topic/PowerShell_CmdLets_to_manage_the_BizTalk_Service.md), and the tasks that can be performed using the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

||Using the Object Model <br /> <br />|Using the PowerShell Cmdlets <br /> <br />|Using the Portal <br /> <br />|
|-|--------------------------|--------------------------------|--------------------|
|Create Partner <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Create Profile <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Add Identities <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Upload Certificate <br /> <br />||√ <br /> <br />|√ <br /> <br />|
|Create X12 Agreement <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Set Partner1, Partner2 <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Add Identities <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Upload Schema <br /> <br />||√ <br /> <br />|√ <br /> <br />|
|--- Create Batch <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|Deploy X12 [!INCLUDE[bridge](/Token/bridge_md.md)]s <br /> <br />|||√ <br /> <br />|
|--- Add Route Settings <br /> <br />|||√ <br /> <br />|
|--- Upload Transform <br /> <br />||√ <br /> <br />|√ <br /> <br />|
|Create AS2 Agreement <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Set Partner1, Partner2 <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|Deploy AS2 [!INCLUDE[bridge](/Token/bridge_md.md)]s <br /> <br />|||√ <br /> <br />|
|--- Add Route Settings <br /> <br />|||√ <br /> <br />|
|Create EDIFACT Agreement <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Set Partner1, Partner2 <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Add Identities <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|--- Upload Schema <br /> <br />||√ <br /> <br />|√ <br /> <br />|
|--- Create Batch <br /> <br />|√ <br /> <br />||√ <br /> <br />|
|Deploy EDIFACT [!INCLUDE[bridge](/Token/bridge_md.md)]s <br /> <br />|||√ <br /> <br />|
|--- Add Route Settings <br /> <br />|||√ <br /> <br />|
|--- Upload Transform <br /> <br />||√ <br /> <br />|√ <br /> <br />|

## <a name="BKMK_TPMEndpoint"></a>Connecting to the TPM OM API REST Endpoint
To retrieve the metadata about TPM OM entities, you can simply hit the endpoint in a browser. However, if you want to perform any CRUD operations on the entities, you must request messages that include the required header values as well as message payload (if required).

- You must include the required headers for invoking the REST endpoint.

   TPM OM API enables users to send OData-based HTTP requests to create TPM OM entities and receive responses in verbose JSON, atom+pub, or straight XML. Because the TPM OM API conforms to [!INCLUDE[azure_2](/Token/azure_2_md.md)] design guidelines, there is a set of required HTTP headers that each client must use when connecting to the TPM OM API REST endpoint, as well as a set of optional headers that can be used. The following sections describe the headers and HTTP verbs you can use with the TPM OM API.

   For a list of required and optional headers, see the HTTP Request, HTTP Response, and HTTP Verbs sections (in this topic).

- Wherever applicable, you must include the required property names with appropriate values. For a list of entities and their properties, see [TPM OM API: Exposed Entities and Properties](/Topic/TPM_OM_API__Exposed_Entities_and_Properties.md).

### Supported HTTP Request Headers
Every call made to the TPM OM API REST endpoints must include a set of required headers and also a set of optional headers, if you want to. The following table lists the required headers:

**Required Headers**

|Header <br /> <br />|Type <br /> <br />|Value <br /> <br />|
|----------|--------|---------|
|Authorization <br /> <br />|WRAP [!INCLUDE[ac2](/Token/ac2_md.md)] tokens <br /> <br />|The value must include the access token provided by the [!INCLUDE[firstref_acs](/Token/firstref_acs_md.md)]. To retrieve an [!INCLUDE[ac2](/Token/ac2_md.md)] token using the WRAP protocol, see [http://msdn.microsoft.com/library/windowsazure/hh674475.aspx](http://msdn.microsoft.com/library/windowsazure/hh674475.aspx). <br /> <br />|
|Host <br /> <br />|String <br /> <br />|Specifies the host and the port number of the resource being targeted. <br /> <br />|
|DataServiceVersion <br /> <br />|Decimal <br /> <br />|1.0 <br /> <br />|
|MaxDataServiceVersion <br /> <br />|Decimal <br /> <br />|3.0 <br /> <br />|
|x-ms-version <br /> <br />|Decimal <br /> <br />|1.0 <br /> <br />|
|If-Match <br /> <br />|Entity tag <br /> <br />|Specifies that an operation is performed only if the entity tag specified in the request header matches with the entity tag of the object. **Note:** This header is required only when performing update or delete operations. <br />|
> [!NOTE]
> Because the TPM OM API uses OData to expose its underlying asset metadata repository through REST APIs, the **DataServiceVersion** and **MaxDataServiceVersion** headers should be included in any request. If they are not included, then currently the TPM OM API assumes the DataServiceVersion value in use is 1.0.

**Optional Headers**

|Header <br /> <br />|Type <br /> <br />|Value <br /> <br />|
|----------|--------|---------|
|Date <br /> <br />|RFC 1123 date <br /> <br />|Timestamp of the request <br /> <br />|
|Accept <br /> <br />|Content type <br /> <br />|The requested content type for the response such as the following: <br /> <br /><ul><li>application/xml </li><li>application/json;odata=verbose </li><li>application/atom+xml </li> </ul>|
|Accept-Encoding <br /> <br />|Gzip, deflate <br /> <br />|GZIP and DEFLATE encoding, when applicable. <br /> <br />|
|Accept-Language <br /> <br />|"en", "es", and so on <br /> <br />|Specifies the preferred language of the response. <br /> <br />|
|Accept-Charset <br /> <br />|Charset type like UTF-8 <br /> <br />|Default is UTF-8 <br /> <br />|
|X-HTTP-Method <br /> <br />|HTTP Method <br /> <br />|Allows clients or firewalls that do not support HTTP methods like PUT or DELETE to use these methods, tunneled via a GET call. <br /> <br />|
|Content-Type <br /> <br />|Content type <br /> <br />|Content type of the request body in POST and PUT requests. <br /> <br />|

### Supported HTTP Response Headers
The following is a set of headers that may be returned to you depending on the resource you were requesting and the action you intended to perform.

|Header <br /> <br />|Type <br /> <br />|Value <br /> <br />|
|----------|--------|---------|
|Date <br /> <br />|RFC 1123 date <br /> <br />|The date that the request was processed <br /> <br />|
|Content-Type <br /> <br />|Varies <br /> <br />|The content type of the response body <br /> <br />|
|Content-Encoding <br /> <br />|Varies <br /> <br />|Gzip or deflate, as appropriate <br /> <br />|
|Cache-Control <br /> <br />|- <br /> <br />|Specifies whether caching mechanisms, from server to client, may cache the object. <br /> <br />|
|Content-Length <br /> <br />|Content type <br /> <br />|The length of the response body <br /> <br />|
|Server <br /> <br />|- <br /> <br />|A server name. <br /> <br />|
|X-Content-Type-Options <br /> <br />|Content type <br /> <br />|The only possible value “nonsniff” prevents browsers from MIME-sniffing a response from the declared content-type. <br /> <br />|

### Supported HTTP Verbs
The following is a complete list of HTTP verbs that are supported by the TPM OM API and can be used when making HTTP requests:

|VERB <br /> <br />|Description <br /> <br />|
|--------|---------------|
|GET <br /> <br />|Returns the current value for an entity <br /> <br />|
|POST <br /> <br />|Creates an object (or submits a command) based on the provided data <br /> <br />|
|PUT <br /> <br />|Replaces an object, or creates a new object (when applicable) <br /> <br />|
|DELETE <br /> <br />|Deletes an object <br /> <br />|
|MERGE <br /> <br />|Updates an existing object with named property changes. <br /> <br />|

## <a name="BKMK_TPMNetApps"></a>Creating .NET Applications Using the TPM OM API
Because the TPM OM API is based on the OData protocol, you can use the WCF Data Services to build .NET applications that perform CRUD operations on the entities. For more information on how create .NET applications using the TPM OM API, see [Creating .NET Applications Using TPM OM REST API](/Topic/Creating_.NET_Applications_Using_TPM_OM_REST_API.md).

## See Also
[Trading Partner Management Object Model &#40;TPM OM&#41;: API Reference](/Topic/Trading_Partner_Management_Object_Model__TPM_OM):%20API%20Reference.md)

