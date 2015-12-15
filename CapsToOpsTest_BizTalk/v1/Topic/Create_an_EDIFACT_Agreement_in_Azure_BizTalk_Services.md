---
description: na
keywords: na
pagetitle: Create an EDIFACT Agreement in Azure BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2cc7653d-20e9-4964-86ea-5146780ee64c
---
# Create an EDIFACT Agreement in Azure BizTalk Services
The topics in this section list the steps to create an EDIFACT agreement.

## Configure EDIFACT General Settings

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, select **Agreements**.

2. On the Agreements page, select the **EDI** tab, and then select **Add**.

3. In the **New Agreement** page, enter the following:

   |||
   |-|-|
   |**Field** <br /> <br />|**Description** <br /> <br />|
   |Name <br /> <br />|Enter a unique name for the agreement. <br /> <br />|
   |Protocol <br /> <br />|Select **EDIFACT** for EDIFACT agreements. <br /> <br />|
   |Description <br /> <br />|Enter notes or a description of the agreement. <br /> <br />|
   |Hosted Partner <br /> <br />|Select the hosted partner for the agreement.  Hosted partner is the partner that [!INCLUDE[af_integration](/Token/af_integration_md.md)] deploys the EDIFACT send and receive pipelines. <br /> <br />The default profile is displayed in the Profile field. Choose the desired profile which has been configured for the partner. <br /> <br />|
   |Guest Partner <br /> <br />|Select the partner for the agreement. A guest partner is the partner that the hosted partner wants to achieve B2B messaging. <br /> <br />The default profile is displayed in the Profile field. Choose the desired profile which has been configured for the partner. <br /> <br />|
   **Identities**

   |||
   |-|-|
   |Hosted Partner Identification <br /> <br />|Enter an identification value for the hosted partner. This can be an alphanumeric value ranging between 1 and 35 characters. <br /> <br />|
   |Hosted Partner Code Qualifier <br /> <br />|Select a business identity code qualifier that provides unique business identities to the trading partners. Trading partners can opt for a mutually agreed business identity. <br /> <br />|
   |Guest Partner Identification <br /> <br />|Enter an identification value for the guest partner. This can be an alphanumeric value ranging between 1 and 35 characters. <br /> <br />|
   |Guest Partner Code Qualifier <br /> <br />|Select a business identity code qualifier that provides unique business identities to the trading partners. Trading partners can opt for a mutually agreed business identity. <br /> <br />|

4. Select **Continue**. The **Receive Settings** and **Send Settings** tabs are added. Each tab creates a one-way agreement between the two partners: one to receive messages from the guest partner and another for sending messages to the guest partner.

## Configure EDIFACT Receive Settings
The receive settings for an EDIFACT agreement primarily include the EDIFACT protocol settings. These settings are used while receiving an EDIFACT message from a trading partner. The **Receive Settings** tab is displayed after you enter the **General Settings** for the agreement.

The **Protocol** page allows you to enter the EDIFACT protocol settings between the two partners. These can be divided into Basic and Advanced settings.

### Basic Settings
**Identifiers**

|||
|-|-|
|**Field** <br /> <br />|**Description** <br /> <br />|
|UNB6.1 (Recipient Reference Password) <br /> <br />|Enter an alphanumeric value ranging between 1 and 14 characters. <br /> <br />|
|UNB6.2 (Recipient Reference Qualifier <br /> <br />|Enter an alphanumeric value with a minimum of one character and a maximum of two characters. <br /> <br />|
**Acknowledgements**

|||
|-|-|
|Receipt of Message (CONTRL) <br /> <br />|Select this checkbox to return a technical (CONTRL) acknowledgment to the interchange sender. The acknowledgment is sent to the interchange sender based on the Send Settings for the agreement. <br /> <br />|
|Acknowledgement (CONTRL) <br /> <br />|Select this checkbox to return a functional (CONTRL) acknowledgment to the interchange sender The acknowledgment is sent to the interchange sender based on the Send Settings for the agreement. <br /> <br />|
**Schemas**

|||
|-|-|
|UNH2.1 (TYPE) <br /> <br />|Select a transaction set type. <br /> <br />|
|UNH2.2 (VERSION) <br /> <br />|Enter the message version number. (Minimum, one character; maximum, three characters). <br /> <br />|
|UNH2.3 (RELEASE) <br /> <br />|Enter the message release number. (Minimum, one character; maximum, three characters). <br /> <br />|
|UNH2.5 (ASSOCIATED ASSIGNED CODE) <br /> <br />|Enter the assigned code. (Maximum, six characters. Must be alphanumeric). <br /> <br />|
|UNG2.1 (APP SENDER ID) <br /> <br />|Enter an alphanumeric value with a minimum of one character and a maximum of 35 characters. <br /> <br />|
|UNG2.2 (APP SENDER CODE QUALIFIER) <br /> <br />|Enter an alphanumeric value, with a maximum of four characters. <br /> <br />|
|SCHEMA <br /> <br />|Choose or upload a schema. The receive pipeline disassembles the incoming message by matching the values for the different fields in the incoming message with the values you set here, and the schema of the incoming message with the schema you set here. To upload a schema: <br /> <br /><ol><li>Select the **Upload** button. </li><li>In the Open dialog box, select the schema to use in the agreement, and select **Open**. **Note:**    Common B2B Schemas are available for download at [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057) </li> </ol>|

### Advanced Settings
**Control Numbers**

|||
|-|-|
|**Field** <br /> <br />|**Description** <br /> <br />|
|Disallow Interchange Control Number duplicates <br /> <br />|Select this checkbox to block duplicate interchanges. If selected, the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] checks that the interchange control number (UNB5) for the received interchange does not match the interchange control number. If a match is detected, then the receive pipeline does not process the interchange. <br /> <br />If you opted to disallow duplicate interchange control numbers, you can specify the number of days at which the check is performed by giving the appropriate value for **Check for duplicate UNB5 every x days** option. <br /> <br />|
|Disallow Group control number duplicates <br /> <br />|Select this checkbox to block interchanges with duplicate group control numbers (UNG5). <br /> <br />|
|Disallow Transaction set control number duplicates <br /> <br />|Select this checkbox to block interchanges with duplicate transaction set control numbers (UNH1). <br /> <br />|
|EDIFACT Acknowledgement Control Number <br /> <br />|To designate the transaction set reference numbers to be used in an acknowledgment, enter a value for the prefix, a range of reference numbers, and a suffix. <br /> <br />|
**Validation**

|||
|-|-|
|Message Type <br /> <br />|Select the message type. <br /> <br />Select the **+** sign to add validation rules for other message types. If no rules are specified, then the row marked as default is used for validation. <br /> <br />|
|EDI Validation <br /> <br />|Select this check box to perform EDI validation on data types as defined by the EDI properties of the schema, length restrictions, empty data elements, and trailing separators. <br /> <br />|
|Extended Validation <br /> <br />|Select this check box to enable extended (BizTalk XSD) validation of interchanges received from the interchange sender. This includes validation of field length, optionality, and repeat count in addition to XSD data type validation. <br /> <br />|
|Allow Leading/Trailing Zeroes <br /> <br />|Select **Allow** to allow leading/trailing zeros; **NotAllowed** to not allow leading/trailing zeros, or **Trim** to trim the leading and trailing zeroes. <br /> <br />|
|Trailing Separator Policy <br /> <br />|<ul><li>Select **Not Allowed** if you do not want to allow trailing delimiters and separators in an interchange received from the interchange sender. If the interchange contains trailing delimiters and separators, it is declared invalid. </li><li>Select **Optional** to accept interchanges with or without trailing delimiters and separators. </li><li>Select **Mandatory** if the received interchange must contain trailing delimiters and separators. </li> </ul>|
**Internal Settings**

|||
|-|-|
|Create empty XML tags if trailing separators are allowed <br /> <br />|Select this check box to have the interchange sender include empty XML tags for trailing separators. <br /> <br />|
|Use dot (.) as decimal separator <br /> <br />|Select this check box to include a dot (.) in the XML message created out of an interchange that contains a decimal number. <br /> <br />|
|Inbound batching processing <br /> <br />|Options include: <br /> <br /><ul><li>**Split Interchange as Transaction Sets - suspend Transaction Sets on Error** (Default): Parses each transaction set in an interchange into a separate XML document by applying the appropriate envelope to the transaction set. With this option, if one or more transaction sets in the interchange fail validation, then [!INCLUDE[af_integration](/Token/af_integration_md.md)] suspends only those transaction sets. </li><li>**Split Interchange as Transaction Sets - suspend Interchange on Error**: Parses each transaction set in an interchange into a separate XML document by applying the appropriate envelope. With this option, if one or more transaction sets in the interchange fail validation, then [!INCLUDE[af_integration](/Token/af_integration_md.md)] suspends the entire interchange. </li><li>**Preserve Interchange - suspend Transaction Sets on Error**: Leaves the interchange intact, creating an XML document for the entire batched interchange. With this option, if one or more transaction sets in the interchange fail validation, then [!INCLUDE[af_integration](/Token/af_integration_md.md)] suspends only those transaction sets, while continuing to process all other transaction sets. </li><li>**Preserve Interchange - suspend Interchange on Error**: Leaves the interchange intact, creating an XML document for the entire batched interchange. With this option, if one or more transaction sets in the interchange fail validation, then [!INCLUDE[af_integration](/Token/af_integration_md.md)] suspends the entire interchange. </li> </ul>|
**Character Sets and Separators**

|||
|-|-|
|UNA1 (Component data element separator) <br /> <br />|Enter a value for the component data element separator that separates simple data elements within composite data elements. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
|UNA2 (Data element separator) <br /> <br />|Enter a value for the data element separator that separates composite data elements consisting of two or more simple data elements or simple data elements that are not part of a composite. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
|UNA3 (Decimal notation) <br /> <br />|Select whether you want to use a **Comma** or **Decimal** as the decimal notation to be used in the outgoing interchange. <br /> <br />|
|UNA4 (Release Indicator) <br /> <br />|Enter a value for the release indicator that indicates that the following character is not a syntax separator, terminator, or release character, but is part of the original data. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
|UNA5 (Repetition Separator) <br /> <br />|Enter a value for the repetition separator to separate segments that repeat within a transaction set. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
|UNA6 (Segment Terminator) <br /> <br />|Enter a value for the segment terminator that indicates the end of an EDI segment. Select **Char** for a character data element or **Hex** for a hexadecimal data element. The character you enter automatically changes if you change its format. <br /> <br />|
|Suffix <br /> <br />|Select whether you want to use carriage return (CR), line feed (LF), both, or none as the end-of-line character that is used with the segment terminator. <br /> <br />|
|||

## Configure EDIFACT Send Settings
The EDIFACT send settings configure the agreement configuration for sending messages from hosted partner to guest partner, and batching and protocol settings. These sections list the steps to configure the send-side settings of an EDIFACT agreement. The **Send Settings** tab is displayed only after you entered the **General Settings**.

### Add a Batch
The **Batching** page on the **Send Settings** tab allows you to create batches to send several messages as a batch to a partner. You can also enter rules based on which batch is triggered. These rules are based on the values of promoted properties you defined in the earlier stages.

1. On the **Batching** page, select **Add Batch** to launch a wizard.

2. In the **Batch details** page, enter a batch name and a batch description, and then select **Next**.

3. In the **Batch criteria** page, enter the criteria based on which a batch configuration is triggered. The batch criterion is specified using the values of the promoted properties at runtime. You can either select the value from a grid to specify the batching condition or use a standard SQL 92 syntax to define the batching condition. To understand this better, let us assume you promoted a property (P1) whose value is set to ‘100’ at runtime. To use this property as a condition for triggering a batch, you can do either of the following:

   - Select the option for the grid, and then select the (**+**) icon to select the property you promoted. From the grid, select **P1**, enter the **Operation** as (**==**), and set the value to **100**.

      OR

   - Select the **Use advanced definitions** option, and specify a SQL 92 expression, such as:

      ```
      P1 == 100
      ```
      You can use this option to provide more detailed query expressions using other operators as well. In the example used here, during the agreement processing if a property P1 is created and its value is set to 100, then this batch is triggered.

   Select **Next**.

4. In the **Batch release criteria** page, enter the criteria for batching messages together. The drop-down lets you select more than one criterion for batching. However, there are four key criterion that can be used together to provide different combinations:

   - **InterchangeSizeBased** – For the **Size(max)** property, enter the number of characters to create and send a batch. The agreement accumulates batching elements until the character count in those elements exceeds the specified character count.

   - **MessageCountBased** – For the **Count** property, enter the number of messages that must be processed together as a batch.

   - **ScheduleBased** – For this option, enter the following properties:

      - **Occurs** – Specifies the unit of measurement of time in terms of minutes, hours, days, or weeks.

      - **First release** – Specifies which day and at what time the first batch is released.

      - **Recurs every** – Specifies the frequency or recurrence, after the first occurrence. For example, if you set this property to **2** and the **Occurs** property to **Hourly**, then the messages are batched every 2 hours after the first release.

      > [!NOTE]
      > There could be a variation of +/- 10 seconds while releasing batches based on these criteria. Also, the time period starts when the first message is received by the bridge.

   - **TimeoutBased** – This property specifies the timeout (in minutes) at which a batch is triggered, irrespective of whether any other criterion is met or not. This property is always used along with another property. For example, if you set the batch release criteria to **MessageSizeBased, TimeoutBased** and the values to **3** messages and **5** minutes respectively, then the agreement first waits to collect three messages to constitute a batch. If three messages do not arrive in 5 minutes, the agreement goes ahead and processes the batch with whatever number of messages that is available. Note that the timeout value is the idle time from the last released batch. For the first batch, this timeout is the idle time from the start of the batch.

      > [!NOTE]
      > There could be a variation of +/- 10 seconds while releasing batches based on these criteria. Also, the time period starts when the first message is received by the bridge.

   You can select different combinations of these key criterions to define when a batch is released.

5. In the **Summary** page, verify the batch configuration and then select **Save**.

   Certain points to consider regarding batches:

   - When you finish these steps, a batch is created. A batch is deployed only when you deploy the agreement containing the batch.

   - You cannot edit a batch when the agreement is deployed. To edit a batch, you must first stop the batch by select the **Stop Batch** link next to the batch.

   - Once you finish editing a batch, you must redeploy the agreement to ensure that the updated batch configuration is used for further batch processing.

   - If you are redeploying an agreement, you do not need to stop the batches associated with it. However, you must ensure that the changes that are made to the agreement do not affect the running batches. For example, if an agreement is updated to not process a specific schema, then you must ensure that none of the running batches are processing a message of that schema. If such batches are not stopped, the messages are suspended when the batch is released.

   - Before you delete an agreement, you must stop any batches associated with the agreement.

### Enter the Protocol settings
The **Protocol** page of the **Send Settings** tab allows you to enter the protocol settings between the two partners. The settings you enter on this page are used to create an EDIFACT message before it is sent to the guest partner. These settings can be divided into Basic and Advanced settings.

#### Basic Settings
**Identifiers**

|||
|-|-|
|UNB1.2 (Syntax version) <br /> <br />|Select a value between **1** and **4**. <br /> <br />|
|UNB2.3 (Sender Reverse Routing Address) <br /> <br />|Enter an alphanumeric value with a minimum of one character and a maximum of 14 characters. <br /> <br />|
|UNB3.3 (Recipient Reverse Routing Address) <br /> <br />|Enter an alphanumeric value with a minimum of one character and a maximum of 14 characters. <br /> <br />|
|UNB6.1 (Recipient Reference Password) <br /> <br />|Enter an alphanumeric value with a minimum of one and a maximum of 14 characters. <br /> <br />|
|UNB6.2 (Recipient Reference Qualifier) <br /> <br />|Enter an alphanumeric value with a minimum of one character and a maximum of two characters. <br /> <br />|
|UNB7 (Application Reference ID) <br /> <br />|Enter an alphanumeric value with a minimum of one character and a maximum of 14 characters <br /> <br />|
**Acknowledgements**

|||
|-|-|
|Receipt of Message (CONTRL) <br /> <br />|Select this checkbox if the hosted partner expects to receive to receive a technical (CONTRL) acknowledgment. This setting specifies that the hosted partner, who is sending the message, requests an acknowledgement from the guest partner. <br /> <br />|
|Acknowledgement (CONTRL) <br /> <br />|Select this checkbox if the hosted partner expects to receive a functional (CONTRL) acknowledgment. This setting specifies that the hosted partner, who is sending the message, requests an acknowledgement from the guest partner. <br /> <br />|
|Generate SG1/SG4 loop for accepted transaction sets <br /> <br />|If you chose to request a functional acknowledgement, select this checkbox to force generation of SG1/SG4 loops in functional CONTRL acknowledgments for accepted transaction sets. <br /> <br />|
**Schemas**

|||
|-|-|
|UNH2.1 (TYPE) <br /> <br />|Select a transaction set type. <br /> <br />|
|UNH2.2 (VERSION) <br /> <br />|Enter the message version number. <br /> <br />|
|UNH2.3 (RELEASE) <br /> <br />|Enter the message release number. <br /> <br />|
|SCHEMA <br /> <br />|Choose a schema to specify how the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] converts the XML message to EDIFACT before sending it to the guest partner. To upload a schema: <br /> <br /><ol><li>Select the **Upload** button. </li><li>In the Open dialog box, select the schema to use in the agreement, and select **Open**. **Note:**    Common B2B schemas are available for download at [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057). </li> </ol>|

#### Advanced Settings
**Envelopes**

|||
|-|-|
|UNB8 (Processing Priority Code) <br /> <br />|Enter an alphabetical value which is not more than one character long. <br /> <br />|
|UNB10 (Communication Agreement) <br /> <br />|Enter an alphanumeric value with a minimum of one character and a maximum of 40 characters. <br /> <br />|
|UNB11 (Test Indicator) <br /> <br />|Select this checkbox to indicate that the interchange generated is test data <br /> <br />|
|Apply UNA Segment (Service String Advice) <br /> <br />|Select this checkbox to generate a UNA segment for the interchange to be sent. <br /> <br />|
|Apply UNG Segments (Function Group Header) <br /> <br />|Select this checkbox to create grouping segments in the functional group header in the messages sent to the guest partner. The following values are used to create the UNG segments: <br /> <br /><ul><li>For **UNG1**, enter an alphanumeric value with a minimum of one character and a maximum of six characters. </li><li>For **UNG2.1**, enter an alphanumeric value with a minimum of one character and a maximum of 35 characters. </li><li>For **UNG2.2**, enter an alphanumeric value, with a maximum of four characters. </li><li>For **UNG3.1**, enter an alphanumeric value with a minimum of one character and a maximum of 35 characters. </li><li>For **UNG3.2**, enter an alphanumeric value, with a maximum of four characters. </li><li>For **UNG6**, enter an alphanumeric value with a minimum of one and a maximum of three characters. </li><li>For **UNG7.1**, enter an alphanumeric value with a minimum of one character and a maximum of three characters. </li><li>For **UNG7.2**, enter an alphanumeric value with a minimum of one character and a maximum of three characters. </li><li>For **UNG7.3**, enter an alphanumeric value with a minimum of 1 character and a maximum of 6 characters. </li><li>For **UNG8**, enter an alphanumeric value with a minimum of one character and a maximum of 14 characters. </li> </ul>|
**Character Set and Separators**

Other than the UNB 1.1 system identifier, you can specify a different set of delimiters to be used for each message type. If a character set is not specified for a given message schema, then the default character set is used.

|||
|-|-|
|UNB1.1 (System Identifier) <br /> <br />|Select the EDIFACT character set to be applied on the outgoing interchange <br /> <br />|
|Schema <br /> <br />|Select the (+) symbol and select a schema from the drop-down list. For the selected schema, select the separators set to be used: <br /> <br /><ul><li>**UNA1 (Component data element separator)** – Enter a value for the component data element separator that separates simple data elements within composite data elements. Default value is (**:**). </li><li>**UNA2 (Data element separator)** – Enter a value for the data element separator that separates composite data elements consisting of two or more simple data elements or simple data elements that are not part of a composite. Default value is (**+**). </li><li>**UNA3 (Decimal notation)** – Specify whether you want to use a **Comma** or **Decimal** as the decimal notation to be used in the outgoing interchange. Default value is **Comma**. </li><li>**UNA4 (Release Indicator)** – Enter a value for the release indicator that indicates that the following character is not a syntax separator, terminator, or release character, but is part of the original data. Default value is (**?**). </li><li>**UNA5 (Repetition Separator)** – Enter a value for the repetition separator that is used to separate segments that repeat within a transaction set. Default value is (**&#42;**). </li><li>**UNA6 (Segment Terminator)** – Enter a value for the segment terminator that indicates the end of an EDI segment. Default value is (**‘**). </li><li>**Suffix** – Specify whether you want to use carriage return (CR), line feed (LF), both, or none as the end-of-line character that is used with the segment terminator. Default value is **None**. </li> </ul>|
**Control Numbers**

|||
|-|-|
|UNB5 (Interchange Control Number ) <br /> <br />|Enter a prefix, a range of values for the interchange control number, and a suffix. These values are used to generate an outgoing interchange. The prefix and suffix are optional; the control number is required. The control number is incremented for each new message; the prefix and suffix remain the same. <br /> <br />|
|UNG5 (Group Control Number) <br /> <br />|Enter a prefix, a range of values for the interchange control number, and a suffix. These values are used to generate the group control number. The prefix and suffix are optional; the control number is required. The control number is incremented for each new message until the maximum value is reached; the prefix and suffix remain the same. <br /> <br />|
|UNH1 (Message Header Reference Number) <br /> <br />|Enter a prefix, a range of values for the interchange control number, and a suffix. These values are used to generate the message header reference number. The prefix and suffix are optional; the reference number is required. The reference number is incremented for each new message; the prefix and suffix remain the same. <br /> <br />|
**Validation**

|||
|-|-|
|Message Type <br /> <br />|Select the message type. <br /> <br />Select the **+** sign to add validation rules for other message types. If no rules are specified, the row marked as default is used for validation. <br /> <br />|
|EDI Validation <br /> <br />|Select this check box to perform EDI validation on data types as defined by the EDI properties of the schema, length restrictions, empty data elements, and trailing separators. <br /> <br />|
|Extended Validation <br /> <br />|Select this check box to enable extended (BizTalk XSD) validation of interchanges received from the interchange sender. This includes validation of field length, optionality, and repeat count in addition to XSD data type validation. <br /> <br />|
|Allow Leading/Trailing Zeroes <br /> <br />|Select **Allow** to allow leading/trailing zeros; **NotAllowed** to not allow leading/trailing zeros, or **Trim** to trim the leading and trailing zeroes. <br /> <br />|
|Trailing Separator Policy <br /> <br />|<ul><li>Select **Not Allowed** if you do not want to allow trailing delimiters and separators in an interchange received from the interchange sender. If the interchange contains trailing delimiters and separators, it is declared invalid. </li><li>Select **Optional** to accept interchanges with or without trailing delimiters and separators. </li><li>Select **Mandatory** if the received interchange must contain trailing delimiters and separators. </li> </ul>|
Select **Save** to save the agreement.

## See Also
[Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md)

