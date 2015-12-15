---
description: na
keywords: na
pagetitle: Create an AS2 Agreement in Azure BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c437391b-9a64-4a18-bd8d-fc551be72bd4
---
# Create an AS2 Agreement in Azure BizTalk Services
Create an AS2 agreement in [!INCLUDE[af_integration](/Token/af_integration_md.md)] to exchange messages between trading partners using the AS2 protocol.

**AS2 non-EDI messaging**

AS2 messages can be sent to a non-EDI destination or received from a non-EDI destination. This functionality is built into AS2 so you don’t have to worry about the transport protocol. You can use X12, EDIFACT, or other protocols that are not included with [!INCLUDE[af_integration](/Token/af_integration_md.md)]. For example, you receive a non-EDI message from a supplier over AS2. You process the XML data and then transform the message to UBL documents.

Non-EDI messaging is enabled in the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] or in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. To use non-EDI messaging in the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], use any of the following tools in the Toolbox:

- [!INCLUDE[one-way](/Token/one-way_md.md)]

- [!INCLUDE[request_response](/Token/request_response_md.md)]

- Two-Way External Service Endpoint

- Two-Way Relay Endpoint

**AS2 Non-Repudiation of Receipt (NRR)**

AS2 includes Non-Repudiation of Receipt (NRR) support. Non-Repudiation provides proof that a message is valid and authentic. If the message validity is ever questioned, its validity can be proven and possibly legally binding.

For example, you and Contoso agree to non-repudiation. You send an AS2 message to Contoso to purchase *widgets*. Then, you deny sending the message to purchase the widgets from Contoso. With non-repudiation enabled, Contoso can retrieve the message to confirm that you agreed to purchase the widgets.

Non-Repudiation of Receipt (NRR) is enabled in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] and is used for EDI and non-EDI messages.

The topics in this section list the steps to create an AS2 agreement, including Non-Repudiation and non-EDI destinations.

## Configure the AS2 General Settings
The first step to create an AS2 agreement between two trading partners is to enter the partners and their AS2 identities.

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, select **Agreements**.

2. On the Agreements page, select the **AS2** tab. Select **Add**. The **General Settings** tab is displayed.

3. Enter the following properties:

   |||
   |-|-|
   |Name <br /> <br />|**Required**. Enter a unique name for the agreement. <br /> <br />|
   |Description <br /> <br />|Enter notes or a description for the agreement. <br /> <br />|

4. For hosted and guest partners, enter the following:

   **Hosted Partner**

   |||
   |-|-|
   |Partner <br /> <br />|Select the hosted partner for the agreement. A hosted partner is the partner that [!INCLUDE[af_integration](/Token/af_integration_md.md)] deploys the AS2 send and receive pipelines. <br /> <br />|
   |Profile <br /> <br />|The default profile is displayed. Choose the desired profile which has been configured for the partner. <br /> <br />|
   |AS2 Identity <br /> <br />|Enter the AS2 Identity, which is the name to identify the partner. Examples include the company name or the company department. <br /> <br />|
   **Guest Partner**

   |||
   |-|-|
   |Partner <br /> <br />|Select the partner for the agreement. A Guest Partner is a partner managed by the service provider and the pipelines are deployed for that partner during agreement deployment. <br /> <br />|
   |Profile <br /> <br />|The default profile is displayed. Choose the desired profile which has been configured for the partner. <br /> <br />|
   |AS2 Identity <br /> <br />|Enter the AS2 Identity, which is the name to identify the partner. Examples include the company name or the company department. <br /> <br />|

5. Under NRR Status, select the **Enable NRR** checkbox to enable non-repudiation on receipt (NRR) in the agreement. NRR is used when the Hosted Partner and Guest Partner agree to use NRR.

6. Select **Continue**.  The Receive Settings and Send Settings tabs are added. Each tab is used to create a one-way agreement between the two partners: one to receive messages and another for sending messages.

## Configure the AS2 Receive Settings
AS2 receive settings primarily include protocol details such as message signing, encryption, and compression, as well as sending MDNs.

1. Select the **Receive Settings** tab of the AS2 agreement page. The first step is to determine whether the receive settings in the agreement are used **or** the settings in the incoming messages are used. Whether you check or uncheck the **Override receive side agreement settings with those in the incoming AS2 message** governs that.

   |||
   |-|-|
   |Cleared <br /> <br />|Use the settings configured in the agreement. <br /> <br />|
   |Checked <br /> <br />|Use the settings from the incoming messages and override the settings in the agreement. The following settings are always honored in the agreement and never overridden: <br /> <br /><ul><li>MDN Text </li><li>Message should be encrypted </li><li>Message should be signed </li> </ul>|

2. Choose the message settings to use with this agreement or template:

   |||
   |-|-|
   |**Message should be signed** <br /> <br />|This option forces the Guest Partner to sign the AS2 messages with their private certificate before sending the message to the Hosted Partner. <br /> <br />The Guest Partner has a Private Certificate (.pfx). The Guest Partner creates the corresponding public certificate (.cer) and sends it to you, the Service Provider. This corresponding public key certificate (.cer) is uploaded by you to the Guest Partner’s profile. This public key certificate validates the signature of the Guest Partner. <br /> <br />**Certificate**: In the drop down list, choose the Guest Partner’s public certificate (.cer) you uploaded to the Guest Partner’s profile. Incoming messages are checked for the correct signature of the Guest Partner. **Note:** This option cannot be overridden by an incoming message. <br />|
   |**Message should be encrypted** <br /> <br />|This option forces the Guest Partner to encrypt the message being received by the Hosted Partner. <br /> <br />The Hosted Partner has a Private Certificate (.pfx) uploaded to its profile. You create the corresponding public certificate (.cer) and send the public certificate to the Guest Partner. The Guest Partner’s public certificate encrypts the message and the Hosted Partner’s corresponding private certificate decrypts the message. <br /> <br />**Certificate**: In the drop down list, choose the Hosted Partner’s private certificate (.pfx) you added to the Hosted Partner’s profile. Incoming encrypted messages are decrypted using the private key certificate from the Hosted Partner’s profile. **Note:** This option cannot be overridden by an incoming message. <br />|
   |**Message should be compressed** <br /> <br />|Choose this option to compress messages sent from the Guest Partner to the Hosted Partner. <br /> <br />|

3. Choose the acknowledgement settings you want to use with this agreement or template. These settings specify that the Guest Partner requests an acknowledgment message from the Hosted Partner in the agreement. The acknowledgment messages from the Hosted Partner are sent to the Guest Partner based on the **URL** in the Send Settings of this AS2 agreement.

   |||
   |-|-|
   |**MDN Text** <br /> <br />|Enter the text used in the body of the Message Disposition Notification (MDN) receipt. This applies if the message sender requests the MDN or the agreement is configured to send MDN receipts. <br /> <br />|
   **Send MDN**

   This setting configures the agreement to send MDN receipts to the sender, which is the Guest Partner. The sender in the context of the receive settings of the agreement is the Guest Partner.

   The following options are available when sending the MDN to the Guest Partner:

   |||
   |-|-|
   |**Send Signed MDN** <br /> <br />|This option configures whether the MDN receipt is sent to the Guest Partner and is signed by the Hosted Partner’s private key certificate. <br /> <br />You can optionally choose a **MIC algorithm** option. The following **MIC algorithm** options are supported for computing the Received-Content-MIC field of the outgoing MDN for non-repudiation at the Guest Partner: <br /> <br /><ul><li>**MD5** : Received-Content-MIC field populated using the MD5 algorithm. </li><li>**SHA1** (Default) : Received-Content-MIC field populated using the SHA1 algorithm. </li><li>**SHA2-256** : Received-Content-MIC field populated using the SHA2-256 algorithm. </li><li>**SHA2-384** : Received-Content-MIC field populated using the SHA2-384 algorithm. </li><li>**SHA2-512** : Received-Content-MIC field populated using the SHA2-512 algorithm. </li> </ul> **Note:** For security reasons, it is recommended to use a SHA algorithm instead of MD5. <br />|
   |**Send asynchronous MDN** <br /> <br />|Choose this option to send an asynchronous MDN receipt to the Guest Partner. Enter the endpoint **URL** that the Guest Partner receives MDNs. <br /> <br />|
   For information on importing certificates on the computer, see [APPENDIX: BizTalk Services Certificates Overview](/Topic/APPENDIX__BizTalk_Services_Certificates_Overview.md).

## Configure the AS2 Send Settings
AS2 send settings primarily include protocol details such as message signing, encryption, and compression, as well as requesting an MDN.

1. Select the **Send Settings** tab of the AS2 agreement page. Choose the message settings to use with this agreement. These settings are used when sending AS2 messages from the hosted partner to the guest partner:

   |||
   |-|-|
   |**Enable message signing** <br /> <br />|This option signs messages sent from the hosted partner to the guest partner. <br /> <br />The Hosted Partner has a Private Certificate (.pfx) used for signing uploaded to the Hosted Partner’s profile. You create the corresponding public certificate (.cer) and send the public certificate to the Guest Partner. This public key validates the Hosted Partner’s signature to the Guest Partner. <br /> <br />**MIC algorithm** options: <br /> <br /><ul><li>**MD5** </li><li>**SHA1** (default) </li><li>**SHA2-256** </li><li>**SHA2-384** </li><li>**SHA2-512** </li> </ul> **Note:** For security reasons, it is recommended to use a SHA algorithm instead of MD5. <br />**Certificate**: In the drop down list, choose the Hosted Partner’s private certificate (.pfx) you added to the Hosted Partner’s profile. Outgoing messages sent to the Guest Partner are signed with the Hosted Partner’s signing certificate. <br /> <br />|
   |**Enable message encryption** <br /> <br />|This option is used by the Hosted Partner to encrypt AS2 messages using the Guest Partner’s public certificate (.cer). <br /> <br />Your Guest Partner has a Private Certificate (.pfx). The Guest Partner creates the corresponding public certificate (.cer) and sends it to you, the Service Provider. This corresponding public key certificate (.cer) is uploaded by you to the Guest Partner’s profile. Your Hosted Partner’s public certificate encrypts the message and your Guest Partner’s corresponding private certificate decrypts the message. <br /> <br />**Encryption algorithm** options: <br /> <br /><ul><li>**AES-128** </li><li>**AES-192** </li><li>**AES-256** </li><li>**DES3** (default) </li><li>**RC2** </li> </ul> **Note:** For security reasons, it is recommended to use an AES or DES algorithm instead of RC2. <br />**Certificate**: In the drop down list, choose the Guest Partner’s public certificate (.cer) you added to the Guest Partner’s profile. Outgoing messages are encrypted using the public key certificate from the Guest Partner’s profile. <br /> <br />|
   |**Enable message compression** <br /> <br />|Choose this option to compress messages sent from the Hosted Partner to the Guest Partner. <br /> <br />|
   |**Unfold HTTP headers** <br /> <br />|Select this check box to unfold HTTP content-type headers into a single line. <br /> <br />|
   For information on importing certificates on the computer, see [APPENDIX: BizTalk Services Certificates Overview](/Topic/APPENDIX__BizTalk_Services_Certificates_Overview.md).

2. Choose the acknowledge settings you want to use with this agreement or template.  These settings specify that the Hosted Partner requests an acknowledgment message from the Guest Partner in the agreement. The acknowledgment messages from the Guest Partner are sent to the Hosted Partner based on the **Inbound URI URL** in the Receive Settings of the agreement.

   **Request MDN**

   This setting configures the agreement to send MDN receipts to the sender of the original AS2 message, which is the Hosted Partner. Acknowledgements are sent to the Hosted Partner after successful delivery of the AS2 message.

   The following options are available when the Hosted Partner requests a MDN:

   |||
   |-|-|
   |**Request signed MDN** <br /> <br />|This option requests that the MDN receipt is signed with the Guest Partner’s private key. The signature is validated using the Guest Partner’s public key certificate that is uploaded to the Guest Partner’s profile. <br /> <br />|
   |**Request asynchronous MDN** <br /> <br />|This option requests that the MDN receipts are sent asynchronously to the sender of the original AS2 message, which is the Hosted Partner. The asynchronous message is sent to the **Inbound URI URL** for the Hosted Partner. This **Inbound URI URL** is set on the Receive Settings of the agreement. <br /> <br />|

3. Select **Save** to save the agreement.

## Known Issues

- The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] allows you to modify the Qualifier of an Identity when an agreement is configured. This can result in inconsistence properties. For example, there is an agreement using ZZ:1234567 and ZZ:7654321 the Qualifier. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] profile settings, you change ZZ:1234567 to be 01:*ChangedValue*. You open the agreement and 01:*ChangedValue* is displayed instead of ZZ:1234567.

   To modify the Qualifier of an identity, delete the agreement, update **Identities** in the partner profile, and then recreate the agreement.

   > [!WARNING]
   > This behavior impacts X12 and AS2.

- Attachments for AS2 messages are not supported in send or receive. Specifically, attachments are silently ignored and the message body is processed as a regular AS2 message.

## See Also
[Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md)

