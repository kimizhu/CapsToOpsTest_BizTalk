---
description: na
keywords: na
pagetitle: Step 3: Create Agreements Between Partner Profiles
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cde1c5c-8d09-4b17-97af-435af2a19b64
---
# Step 3: Create Agreements Between Partner Profiles
In this step, you create an agreement between the profiles of the two trading partners, Northwind and Contoso.

### To specify the General Settings of an X12 agreement

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Agreements**.

2. On the **Agreements** page, click the **X12** tab if you are not already on that tab. Then click **Add**.

3. In the **New Agreement** page, enter the following details:

   |||
   |-|-|
   |**Field** <br /> <br />|**Description** <br /> <br />|
   |Name <br /> <br />|Enter a name for the agreement. For this tutorial, specify the name as **NorthwindContosoX12**. **Note:** This is a mandatory field. The name for the agreement must be unique. <br />|
   |Description <br /> <br />|Enter notes or a description for the agreement. <br /> <br />|
   |Hosted Partner <br /> <br />|Select the hosted partner for the agreement. A hosted partner is a partner managed by the service provider and the pipelines are deployed for that partner during agreement deployment. Typically partners managed by service provider are configured as a hosted partner while the enterprise partners are guest partners. <br /> <br />For this tutorial, the hosted partner is **Northwind**. The default profile for Northwind is displayed in the **Profile** field. <br /> <br />|
   |Guest Partner <br /> <br />|Select the partner for the agreement (who is not a hosted partner). For this tutorial, select **Contoso**. The default profile for Contoso is displayed in the **Profile** field. <br /> <br />|
   **Identities**

   |||
   |-|-|
   |Hosted Partner ID Qualifier <br /> <br />|Select an authenticating qualifier that provides unique business identities to the trading partners. For this tutorial, select **ZZ-Mutually Defined**. <br /> <br />|
   |Value <br /> <br />|Enter **US**. <br /> <br />|
   |Guest Partner ID Qualifier <br /> <br />|Select an authenticating qualifier that provides unique business identities to the trading partners. For this tutorial, select **ZZ-Mutually Defined**. <br /> <br />|
   |Value <br /> <br />|Enter **THEM**. <br /> <br />|
   **Tracking**

   |||
   |-|-|
   |Track Send side message properties <br /> <br />|Check this to store the message properties when the EDI message is sent to the partner. Once stored, you can query this data by clicking **Tracking** on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page. <br /> <br />When enabled, you can also store the message body by checking **Archive Send side message**. <br /> <br />|
   |Track Receive side message properties <br /> <br />|Check this to store the message properties when the EDI message is received from a partner. Once stored, you can query this data by clicking **Tracking** on the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page. <br /> <br />When enabled, you can also store the message body by checking **Archive Receive side message**. <br /> <br />|

4. Click **Continue**.

   Clicking **Continue** adds two new tabs, one for receive settings and the other for send settings. Each tab is for a one-way agreement between the two partners, one for receiving messages and the other for sending messages. The properties in the **Receive Settings** tab define how the EDI receive bridge is configured. This bridge receives incoming EDI messages that are sent to Northwind. Similarly, the properties in the **Send Settings** tab define how the EDI send bridge is configured. This bridge sends EDI messages from Northwind to its trading partners like Contoso.

### To specify the receive settings

1. On the **Transport** page, set the **Transport type** to HTTP.

2. On the **Protocol** page, specify the following values.

   1. Under **Acknowledgements**, select **TA1 expected** and **997 expected** to receive acknowledgements from the partner receiving the message.

   2. Under the **Schemas** section, set the following properties.

      |||
      |-|-|
      |Version <br /> <br />|00401 <br /> <br />|
      |Transaction Type (ST1) <br /> <br />|840 <br /> <br />|
      |Sender Application (GS2) <br /> <br />|THEM <br /> <br />|
      |Schema <br /> <br />|/X12_00401_840.xsd <br /> <br />|
      > [!NOTE]
      > You do not need to explicitly upload the artifacts (schemas or transforms) to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. The **EAIEDITutorial**[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] you created earlier already includes the artifacts. So, deploying the project also uploads the artifacts under the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. Because you registered with the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] using the same [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription, the artifacts are also available from the portal. You can view the schemas and transforms from the **Resources** tab of the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

3. On the Transform page, click the plus sign to add a new row. From the drop-down, choose **/X12_00401_840.xsd** for **Schemas** and **/EDI840ToSalesOrder.trfm** for **Transform file name**.

4. On the **Route** page, click **Add** to add a route destination.

   1. Set the **Rule Name** to **SendToBridge**.

   2. Under **Route rule**, select the **Use advanced definitions** option and specify the following expression in the text box:

      ```
      1=1
      ```
      This expression always resolves to true, which means that all the messages are routed to the [!INCLUDE[bridge](/Token/bridge_md.md)].

      > [!NOTE]
      > Even if you do not select the **Use advanced definitions** option and do not provide any route rule, by default this option is selected and its value is set to **1=1**. This means that the default behavior is to route all the messages to the route destination.

   3. Under **Route action**, click the plus sign to add a new row and set the following values:

      - Set **Target Type** to **Http Header**

      - Set **Header Name** to **Content-Type**

      - Set **Value Type** to **Constant**

      - Set **Constant Value** to **application/xml**

      > [!NOTE]
      > This ensures that all the messages that are routed to the [!INCLUDE[bridge](/Token/bridge_md.md)] include a **content-type** header with its value set to **application/xml**. Without this header, the bridge receiving the message treats it as a flat-file message and might result in validation errors.

   4. Under **Route destination**, set **Transport type** to **Azure BizTalk Bridge** and in the text box enter the entity name of the bridge on the message flow surface. For this tutorial, the entity name is the default name, which is **XmlRequestReplyBridge1**. Using this name the bridge deployment endpoint is built, which is `http://*mybiztalkservicename*.biztalk.windows.net/default/**XmlRequestReplyBridge1**`. With this configuration, all the messages processed by the agreement are routed to the [!INCLUDE[request_response](/Token/request_response_md.md)] bridge you deployed earlier.

      Click **Save**.

5. On the **Route** page, Under **Message Suspension Settings**, specify an endpoint where any messages that fail processing are sent to. For example, you can set Transport type to **Azure Service Bus**, the route destination type to **BasicHttpRelay**, and then specify a relay endpoint with all the details where a failed message is routed to.

   > [!NOTE]
   > This tutorial does not cover the scenario where a failed message is sent to the endpoint you specify in the **Message Suspension Settings**. However, for successful deployment of the agreement, you must provide a value for this property. You can enter a non-empty value.

### To specify the send settings

1. On the Send Settings tab, leave the default values for Inbound URL, Transform, and Batching pages.

2. On the **Protocol** page, under the **Schemas** section, specify the following properties.

   |||
   |-|-|
   |Version <br /> <br />|00401 <br /> <br />|
   |Transaction Type (ST1) <br /> <br />|840 <br /> <br />|
   |Schema <br /> <br />|/X12_00401_840.xsd <br /> <br />|

3. On the **Transport** page, specify the endpoints where the response messages or acknowledgements received from the other partner will be sent to. You must specify an endpoint each for the messages that are processed successfully as well as the messages that get suspended due to a failure in processing.

   For receiving messages that were successfully processed, under **Transport Settings** specify the following values:

   - Set **Transport type** to **Azure Service Bus**.

   - Set the route destination type to **BasicHttpRelay**,

   - Specify the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace, issuer name, and issuer key for the relay endpoint.

   - Specify the relay endpoint as **Success** so that the entire URL endpoint is `http://*servicebus namespace*.servicebus.windows.net/Success`.

   For receiving messages that failed processing, under **Message Suspension Settings** specify the following values:

   - Set **Transport type** to **Azure Service Bus**.

   - Set the route destination type to **BasicHttpRelay**,

   - Specify the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace, issuer name, and issuer key for the relay endpoint.

   - Specify the relay endpoint as **Failure** so that the entire URL endpoint is `http://*servicebus namespace*.servicebus.windows.net/Failure`.

4. Click **Deploy** to deploy the agreement. The agreement is now deployed at the URL that was displayed in the **Transport** page of the **Receive Settings** tab. Typically, the endpoint where the agreement is deployed resembles the following:

   ```
   https://mybiztalkservicename.biztalk.windows.net/default/Agreements/<AgreementID>/Receive
   ```

## See Also
[Create and Deploy the Trading Partner Agreement](/Topic/Create_and_Deploy_the_Trading_Partner_Agreement.md)

