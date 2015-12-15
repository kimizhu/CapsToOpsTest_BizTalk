---
description: na
keywords: na
pagetitle: Step 5: Create and Deploy the EDI Receive Pipeline
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.service: multiple
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 370548fe-3443-4ae5-ba83-a29faad46b94
---
# Step 5: Create and Deploy the EDI Receive Pipeline
In this topic, you configure the EDI Receive [!INCLUDE[bridge](/Token/bridge_md.md)] that receives an X12 850 PO message from an FTP server, processes it, transforms it to an ORDERS05 IDOC, and then routes it to the [!INCLUDE[one-way](/Token/one-way_md.md)] that you deployed in the previous step.

### To configure an EDI Receive pipeline

1. Log into the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. You can get the URL for the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] from your [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription. For more information about logging into the portal, see [http://go.microsoft.com/fwlink/p/?LinkId=317714](http://go.microsoft.com/fwlink/p/?LinkId=317714).

2. Create a partner for **Fabrikam** and **Contoso**. On the left pane, select **Partners**, and then from the **Partners** page, select **Add Partner**.

3. Create an agreement between the two partners. On the **Agreements** page, select the **EDI** tab if you are not already on that tab. Then click **Add**.

4. Set the following values for the **General Settings** tab.

   TABLE REMOVED

5. Select **Continue**.

   Selecting **Continue** adds two new tabs: one for receive settings and the other for send settings. Each tab is for a one-way agreement between the two partners, one for receiving messages and the other for sending messages. The properties in the **Receive Settings** tab define how the EDI receive bridge is configured. This bridge receives incoming EDI messages that are sent to Fabrikam. Similarly, the properties in the **Send Settings** tab define how the EDI send bridge is configured. This bridge sends EDI messages from Fabrikam to its trading partners like Contoso.

### To specify the receive settings

1. From the agreements page, select the **Receive Settings** tab.

2. Enter the following values for the **Transport** section:

   - For **Transport Type**, select **FTP**. In the scenario used in this tutorial, Contoso sends the X12 850 message using an FTP location.

   - Provide the name of the FTP Server from where the messages are picked.

   - Enter the username and password to connect to the FTP Server.

   - Enter the relative path on the server from where to pick the X12 850 message.

   ![](/Image/AFINT_PG_Recv_FTP.gif)

3. Enter the following values for the **Protocol** section:

   - Enter whether you want to receive technical (TA1) and functional acknowledgements (997).

   - Under **Schemas**, select the plus sign and specify the following values:

      |For this <br /> <br />|Specify this <br /> <br />|
      |------------|----------------|
      |For **Version** <br /> <br />|Specify **00401**. <br /> <br />|
      |For **Transaction Type (ST1)** <br /> <br />|Specify **850 – Purchase Order**. <br /> <br />|
      |For **Sender Application (GS02)** <br /> <br />|Specify **CONTOSO**. <br /> <br />|
      |For **Schema** <br /> <br />|From the drop-down list, select the schema (X12_00401_850.xsd). This schema was uploaded to your [!INCLUDE[af_integration](/Token/af_integration_md.md)] when you deployed the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] in the last step. <br /> <br />|
      ![](/Image/AFINT_PG_Recv_Protocol.gif)

4. In the **Transform** section, select the plus sign to add a transform to the agreement. From the drop-down list, select the X12_00401_850.xsd schema and the transform you created earlier (AzureTransformations.trfm). The schema as well as the transform is deployed to the [!INCLUDE[af_integration](/Token/af_integration_md.md)] subscription when you deployed the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] in the previous step:

   ![](/Image/AFINT_PG_Recv_TRFM.gif)

5. On the **Route** page, under **Route Settings**, select **Add** to add a route destination.

   1. Set the **Rule Name** to **SendToBridge**.

   2. Under **Route rule**, select **Use advanced definitions**, and enter the following expression in the text box:

      ```
      1=1
      ```
      This expression always resolves to true, which means that all the messages are routed to the [!INCLUDE[bridge](/Token/bridge_md.md)].

      > [!NOTE]
      > Even if you do not select the **Use advanced definitions** option and do not provide any route rule, by default this option is selected and its value is set to **1=1**. This means that the default behavior is to route all the messages to the route destination.

   3. Under **Route action**, select the plus sign to add a new row and set the following values:

      - Set **Target Type** to **Http Header**

      - Set **Header Name** to **Content-Type**

      - Set **Value Type** to **Constant**

      - Set **Constant Value** to **application/xml**

      > [!NOTE]
      > This ensures that all the messages that are routed to the [!INCLUDE[bridge](/Token/bridge_md.md)] include a **content-type** header with its value set to **application/xml**. Without this header, the bridge receiving the message treats it as a flat-file message and might result in validation errors.

   4. Under **Route destination**, set **Transport type** to **Azure BizTalk Bridge** and in the text box enter the entity name of the [!INCLUDE[bridge](/Token/bridge_md.md)] on the message flow surface. For this tutorial, you specified the [!INCLUDE[bridge](/Token/bridge_md.md)] name as **B2BConnector**. Using this name the bridge deployment endpoint is built, which is `http://*<mybiztalkservicename>*.biztalk.windows.net/default/**B2BConnector**`. With this configuration, all the messages processed by the agreement are routed to the [!INCLUDE[one-way](/Token/one-way_md.md)] bridge you deployed earlier.

      ![](/Image/AFINT_SAP.gif)

      Select **Save**.

   5. On the **Route** page, under **Message Suspension Settings**, enter the **Transport Type** as **Azure Service Bus**, and then enter the following values:

      - Set the route destination type to **BasicHttpRelay**.

      - Enter the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace, issuer name, and issuer key.

      - Enter the endpoint URL where a relay receiver service is already running. For this tutorial, specify this as **Suspend**. So, the complete URL where a failed message is sent is `http://*<servicebus_namespace>*.servicebus.windows.net/Suspend`.

### To specify the send settings

1. From the agreements page, select the **Send Settings** tab.

   > [!NOTE]
   > Even though this tutorial does not cover the send side of the agreement, you must specify the minimum default values to successfully deploy the agreement.

2. Retain the default values **Inbound URL**, **Transform**, and **Batching** tabs.

3. In the **Protocol** tab, under **Schemas**, enter the following values:

   |Property <br /> <br />|Description <br /> <br />|
   |------------|---------------|
   |For **Version** <br /> <br />|Set this to **00401** <br /> <br />|
   |For **Transaction Type (ST01)** <br /> <br />|Set this to **850 – Purchase Order** <br /> <br />|
   |For **Schema** <br /> <br />|Set this to **X12_00401_850**. <br /> <br />|

4. In the **Transport** section, under **Transport Settings**, enter the following values:

   - Set the **Transport Type** to **FTP/S**.

   - Enter the required values for the FTP transport.

5. In the **Transport** section, under **Message Suspension Settings**, enter the following values:

   - Set the **Transport Type** to **Azure Service Bus**.

   - Set the route destination type to **BasicHttpRelay**.

   - Specify the [!INCLUDE[sb2](/Token/sb2_md.md)] namespace, issuer name, and issuer key.

   - Specify the endpoint URL where a relay receiver service is already running. For this tutorial, specify this as **Suspend**. So, the complete URL where a failed message is sent is `http://*<servicebus_namespace>*.servicebus.windows.net/Send_Failure`.

6. Select **Deploy Agreement** to deploy the agreement.

   Once the agreement is deployed, to test the solution, you can go ahead and drop a test PO 850 message in the folder on the FTP server that you specified as part of the agreement. More details on how to test the solution are provided in the next topic, [Step 6: Test the Solution](/Topic/Step_6__Test_the_Solution.md).

## See Also
[Tutorial: Using Azure BizTalk Services to Integrate with an On-Premises SAP Server](/Topic/Tutorial__Using_Azure_BizTalk_Services_to_Integrate_with_an_On-Premises_SAP_Server.md)

