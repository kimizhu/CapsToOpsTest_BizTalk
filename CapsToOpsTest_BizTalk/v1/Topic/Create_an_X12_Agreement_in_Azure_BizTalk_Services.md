---
description: na
keywords: na
pagetitle: Create an X12 Agreement in Azure BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a52d83c-900a-4ec8-ae3d-44328059f6b3
---
# Create an X12 Agreement in Azure BizTalk Services
The topic shows how to create an X12 agreement in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

## Create an X12 Agreement
To create an X12 agreement between two trading partners, enter the partners and their identities.

1. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, select **Agreements**.

2. On the Agreements page, select the **EDI** tab, and then select **Add**.

3. In the **New Agreement** page, enter the following:

   |||
   |-|-|
   |**Field** <br /> <br />|**Description** <br /> <br />|
   |Name <br /> <br />|Enter a unique name for the agreement. <br /> <br />|
   |Protocol <br /> <br />|Select **X12** for X12 agreements. <br /> <br />|
   |Description <br /> <br />|Enter notes or a description of the agreement. <br /> <br />|
   |Hosted Partner <br /> <br />|Select the hosted partner for the agreement.  Hosted partner is the partner that [!INCLUDE[af_integration](/Token/af_integration_md.md)] deploys the X12 send and receive pipelines. <br /> <br />|
   |Guest Partner <br /> <br />|Select the partner for the agreement. A guest partner is the partner that the hosted partner wants to use B2B messaging. <br /> <br />|
   **Identities**

   |||
   |-|-|
   |Hosted Partner Qualifier <br /> <br />|Select the business identity qualifier that provides unique business identities to the trading partners. Trading partners can opt for a mutually agreed business identity. <br /> <br />|
   |Hosted Partner Value <br /> <br />|Enter the value for the hosted partner qualifier. <br /> <br />|
   |Guest Partner Qualifier <br /> <br />|Select an business identity qualifier that provides unique business identities to the trading partners. Trading partners can opt for a mutually agreed business identity. <br /> <br />|
   |Guest Partner Value <br /> <br />|Enter the value for the guest partner qualifier. <br /> <br />|

4. Select **Continue**. The **Receive Settings** and **Send Settings** tabs are added. Each tab is to create a one-way agreement between the two partners: one to receive messages and another for sending messages.

## Configure the X12 Receive settings
The receive settings for an X12 agreement primarily include the X12 protocol settings. These settings are used when receiving an X12 message from a trading partner. The **Receive Settings** tab is displayed only after you entered the **General Settings** for the agreement.

You can use the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to receive messages from a trading partner and send back an acknowledgement. To send an acknowledgement in response to a message:

- Select the option to generate technical and functional acknowledgements from the **Protocol** page on the **Receive Settings** tab. By doing this, you declare that the party which sent the interchange expects an acknowledgement.

- If the acknowledgement needs to be sent back with specific properties set, such as CR LF enabled, separator characters to be different, and so on, then set those properties. You can configure this from the **Advanced Settings** section of the **Protocol** page of the **Send Settings** tab. By doing this, you configure how the party sends back the acknowledgement.

In the **Protocol** page, you enter the protocol settings between the two partners. These can be divided into Basic and Advanced Settings.

### Basic Settings
**Identifiers**

|||
|-|-|
|**Field** <br /> <br />|**Description** <br /> <br />|
|ISA1 (Authorization Qualifier) <br /> <br />|Select the Authorization qualifier value from the drop-down list. <br /> <br />|
|ISA2 <br /> <br />|Optional. Enter Authorization information value. If the value you entered for ISA1 is other than 00, enter a minimum of one alphanumeric character and a maximum of 10. <br /> <br />|
|ISA3 (Security Qualifier) <br /> <br />|Select the Security qualifier value from the drop-down list. <br /> <br />|
|ISA4 <br /> <br />|Optional. Enter the Security information value. If the value you entered for ISA3 is other than 00, enter a minimum of one alphanumeric character and a maximum of 10. <br /> <br />|
**Acknowledgements**

|||
|-|-|
|TA1 expected <br /> <br />|Select this checkbox to return a technical (TA1) acknowledgment to the interchange sender. These acknowledgments are sent to the interchange sender based on the Send Settings for the agreement. <br /> <br />|
|FA expected <br /> <br />|Select this checkbox to return a functional (FA) acknowledgment to the interchange sender. Then select whether you want the 997 or 999 acknowledgements, based on the schema versions you are working with. These acknowledgments are sent to the interchange sender based on the Send Settings for the agreement. <br /> <br />|
|Include AK2/IK2 Loop <br /> <br />|Select this checkbox to enable generation of AK2 loops in functional acknowledgments for accepted transaction sets. **Note:** This checkbox is enabled only if you selected the **FA expected** checkbox. <br />|
**Schemas**

|||
|-|-|
||Choose a schema for each transaction type (ST1) and Sender Application (GS2). The receive pipeline disassembles the incoming message by matching the values for ST1 and GS2 in the incoming message with the values you set here, and the schema of the incoming message with the schema you set here. To upload a schema: <br /> <br /><ol><li>Select the **Upload** button. </li><li>In the Open dialog box, select the schema to use in the agreement, and select **Open**. **Note:**    Common B2B Schemas are available to download at [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057). </li><li>Once the schema is uploaded, you can specify the ST1 and GS2 details. </li> </ol>The Receive pipeline is now be able to disassemble any message that conforms to the selected schema. <br /> <br />|

### Advanced Settings
**Control Numbers**

|||
|-|-|
|**Field** <br /> <br />|**Description** <br /> <br />|
|Disallow Interchange Control Number duplicates <br /> <br />|Check this option to block duplicate interchanges. If selected, the BizTalk Services Portal checks that the interchange control number (ISA13) for the received interchange does not match the interchange control number. If a match is detected, the receive pipeline does not process the interchange. <br /> <br />If you opted to disallow duplicate interchange control numbers, then you can specify the number of days at which the check is performed by giving the appropriate value for **Check for duplicate ISA13 every x days**. <br /> <br />|
|Disallow Group control number duplicates <br /> <br />|Check this option to block interchanges with duplicate group control numbers. <br /> <br />|
|Disallow Transaction set control number duplicates <br /> <br />|Check this option to block interchanges with duplicate transaction set control numbers. <br /> <br />|
**Validation**

|||
|-|-|
|Message Type <br /> <br />|EDI Message type, like *850-Purchase Order* or *999-Implementation Acknowledgement*. <br /> <br />|
|EDI Validation <br /> <br />|Performs EDI validation on data types as defined by the EDI properties of the schema, length restrictions, empty data elements, and trailing separators. <br /> <br />|
|Extended Validation <br /> <br />|If the data type is not EDI, validation is on the data element requirement and allowed repetition, enumerations, and data element length validation (min/max). <br /> <br />|
|Allow Leading/Trailing Zeroes <br /> <br />|Any additional space and zero characters that are leading or trailing are retained. They are not removed. <br /> <br />|
|Trailing Separator Policy <br /> <br />|Generates trailing separators on the interchange received. Options include **NotAllowed**, **Optional**, and **Mandatory**. <br /> <br />|
**Internal Settings**

|||
|-|-|
|Convert implied decimal format Nn to base 10 numeric value <br /> <br />|Converts an EDI number that is specified with the format Nn into a base-10 numeric value in the intermediate XML in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. <br /> <br />|
|Create empty XML tags if trailing separators are allowed <br /> <br />|Select this check box to have the interchange sender include empty XML tags for trailing separators. <br /> <br />|
|Inbound batching processing <br /> <br />|Options include: <br /> <br /><ul><li>**Split Interchange as transaction sets - suspend transaction sets on error**: Parses each transaction set in an interchange into a separate XML document by applying the appropriate envelope to the transaction set. With this option, if one or more transaction sets in the interchange fail validation, then [!INCLUDE[af_integration](/Token/af_integration_md.md)] suspends only those transaction sets. </li><li>**Split Interchange as transaction sets - suspend interchange on error**: Parses each transaction set in an interchange into a separate XML document by applying the appropriate envelope. With this option, if one or more transaction sets in the interchange fail validation, then [!INCLUDE[af_integration](/Token/af_integration_md.md)] suspends the entire interchange. </li><li>**Preserve Interchange - suspend transaction sets on error**: Leaves the interchange intact, creating an XML document for the entire batched interchange. With this option, if onAe or more transaction sets in the interchange fail validation, then [!INCLUDE[af_integration](/Token/af_integration_md.md)] suspends only those transaction sets, while continuing to process all other transaction sets. </li><li>**Preserve Interchange - suspend interchange on error**: Leaves the interchange intact, creating an XML document for the entire batched interchange. With this option, if one or more transaction sets in the interchange fail validation, then [!INCLUDE[af_integration](/Token/af_integration_md.md)] suspends the entire interchange. </li> </ul>|

## Configure the X12 Send settings
The X12 send settings specify the agreement configuration for sending messages to trading partners, including batching and protocol settings. This section lists the steps to configure the send-side settings of an X12 agreement. The **Send Settings** tab is displayed only after you have specified the **General Settings**.

### Add a Batch
The **Batching** page on the **Send Settings** tab allows you to create batches to send several messages as a batch to a partner. You can also enter rules based on which a batch is triggered. These rules are based on the values of promoted properties you defined in the earlier stages.

1. On the **Batching** page, select **Add Batch** to launch a wizard.

2. In the **Batch details** page, enter a batch name and a batch description, and then select **Next**.

3. In the **Batch criteria** page, enter the criteria based on which a batch configuration is triggered. The batch criterion is specified using the values of the promoted properties at runtime. You can either select the value from a grid to specify the batching condition or use a standard SQL 92 syntax to define the batching condition. To understand this better, let us assume you promoted a property (P1) whose value is set to ‘100’ at runtime. To use this property as a condition for triggering a batch, you can do either of the following:

   - Select the option for the grid, and then select the (**+**) icon to select the property you promoted. From the grid, select **P1**, specify the **Operation** as (**==**), and set the value to **100**.

      OR

   - Select the **Use advanced definitions** option, and specify a SQL 92 expression, such as:

      ```
      P1 == 100
      ```
      You can use this option to provide more detailed query expressions using other operators as well. In the example used here, during the agreement processing if a property P1 is created and its value is set to 100, then this batch is triggered.

   Select **Next**.

4. In the **Batch release criteria** page, specify the criteria for batching messages together. The drop-down lets you select more than one criterion for batching. However there are four key criterion that can be used together to provide different combinations:

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

5. In the **Summary** page, verify the batch configuration, and then select **Save**.

   Certain points to consider regarding batches:

   - When you finish these steps, a batch is created. A batch is deployed only when you deploy the agreement containing the batch.

   - You cannot edit a batch when the agreement is deployed. To edit a batch you must first stop the batch by selecting the **Stop Batch** link next to the batch.

   - Once you finish editing a batch, you must redeploy the agreement to ensure that the updated batch configuration is used for further batch processing.

   - If you are redeploying an agreement, you do not need to stop the batches associated with it. However, you must ensure that the changes that are made to the agreement do not affect the running batches. For example, if an agreement is updated to not process a purchase order schema (850), then you must ensure that none of the running batches are processing an 850 message at that point in time. If such batches are not stopped, then the messages are suspended when the batch is released.

   - Before you delete an agreement, you must stop any batches associated with the agreement.

### Add the Protocol settings
The **Protocol** page of the **Send Settings** tab allows you to enter the protocol settings between the two partners. These settings are used to create an X12 message before it is sent to the guest partner. These can be divided into Basic and Advanced Settings.

#### Basic Settings
**Identifiers**

|||
|-|-|
|Authorization qualifier (ISA1) <br /> <br />|Select the Authorization qualifier value from the drop-down list. <br /> <br />|
|ISA2 <br /> <br />|Enter Authorization information value. If this value is other than 00, then enter a minimum of one alphanumeric character and a maximum of 10. <br /> <br />|
|Security qualifier (ISA3) <br /> <br />|Select the Security qualifier value from the drop-down list. <br /> <br />|
|ISA4 <br /> <br />|Enter the Security information value. If this value is other than 00, for the Value (ISA4) text box, then enter a minimum of one alphanumeric value and a maximum of 10. <br /> <br />|
**Acknowledgements**

|||
|-|-|
|TA1 expected <br /> <br />|Select this checkbox to return a technical (TA1) acknowledgment to the interchange sender. This setting specifies that the host partner who is sending the message requests an acknowledgement from the guest partner in the agreement. These acknowledgments are expected by the host partner based on the Receive Settings of the agreement. <br /> <br />|
|FA expected <br /> <br />|Select this checkbox to return a functional (FA) acknowledgment to the interchange sender, and then select whether you want the 997 or 999 acknowledgements, based on the schema versions you are working with. These acknowledgments are expected by the host partner based on the Receive Settings of the agreement. <br /> <br />|
**Schemas**

|||
|-|-|
||Choose a schema to determine how the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] converts the XML message to EDI/ X12. The Send pipeline assembles the outgoing message by matching the values of GS and ST segments specified in this page with the GS and ST values in the message and the schema specified in this page with the schema of the XML message. To upload a schema: <br /> <br /><ol><li>Select the **Upload** button. </li><li>In the Open dialog box, select the schema to use in the agreement, and select **Open**. **Note:**    Common B2B schemas are available for download at [http://go.microsoft.com/fwlink/p/?LinkId=235057](http://go.microsoft.com/fwlink/p/?LinkId=235057) </li><li>Once the schema is uploaded, you can specify the ST1 and Version details. </li> </ol>The Send bridge uses these settings to assemble any message that conforms to the selected schema. <br /> <br />|

#### Advanced Settings
**Envelopes**

|||
|-|-|
|ISA11 Usage <br /> <br />|Use this field to specify the separator in a transaction set: <br /> <br /><ul><li>Select the Standard identifier to use the decimal notation of “.” instead of the decimal notation of the incoming document in the EDI receive pipeline. </li><li>Select Repetition separator to specify the separator for repeated occurrences of a simple data element or a repeated data structure. For example, (^) is usually used as repetition separator. For HIPAA schemas, you can only use (^). </li> </ul>|
|Control Version Number (ISA12) <br /> <br />|Select the version of the X12 standard that is used by the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] for generating an outgoing interchange. <br /> <br />|
|Usage Indicator (ISA15) <br /> <br />|Enter whether the context of an interchange is information (I), production data (P), or test data (T). The EDI receive pipeline promotes this property to the context. <br /> <br />|
|Schema <br /> <br />|You can enter how the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] generates the GS and ST segments for an X12-encoded interchange that it sends to the Send Pipeline. <br /> <br />You can associate values of the GS1, GS2, GS3, GS4, GS5, GS7, and GS8 data elements with values of the Transaction Type, and Version/Release data elements. When the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] determines that an XML message has the values set for the Transaction Type, and Version/Release elements in a row of the grid, then it populates the GS1, GS2, GS3, GS4, GS5, GS7, and GS8 data elements in the envelope of the outgoing interchange with the values from the same row of the grid. The values of the Transaction Type, and Version/Release elements must be unique. <br /> <br /><ol><li>Optional. For GS1, select a value for the functional code from the drop-down list. </li><li>Required. For GS2, enter an alphanumeric value for the application sender with a minimum of two characters and a maximum of 15 characters. </li><li>Required. For GS3, enter an alphanumeric value for the application receiver with a minimum of two characters and a maximum of 15 characters. </li><li>Optional. For GS4, select CCYYMMDD or YYMMDD. </li><li>Optional. For GS5, select HHMM, HHMMSS, or HHMMSSdd. </li><li>Optional. For GS7, select a value for the responsible agency from the drop-down list. </li><li>Optional. For GS8, enter an alphanumeric value for the document identified with a minimum of one character and a maximum of 12 characters. **Note:**    These are the values that the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] enters in the GS fields of the interchange it is building if the Transaction Type, and Version/Release elements in the same row are a match for those associated with the interchange. </li> </ol>|
**Character Set and Separators**

Other than the character set, you can enter a different set of delimiters to be used for each message type. If a character set is not specified for a given message schema, then the default character set is used.

|||
|-|-|
|Character Set to be used <br /> <br />|Select the X12 character set to validate the properties that you enter for the agreement. **Note:** The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] only uses this setting to validate the values entered for the related agreement properties. The receive pipeline or send pipeline ignores this character-set property when performing run-time processing. <br />|
|Schema <br /> <br />|Select the (+) symbol and select a schema from the drop-down list. For the selected schema, select the separators set to be used: <br /> <br /><ul><li>**Component element separator** – Enter a single character to separate composite data elements. </li><li>**Data Element Separator** – Enter a single character to separate simple data elements within composite data elements. </li><li>**Replacement Character** – Select this check box if the payload data contains characters that are also used as data, segment, or component separators. You can then enter a replacement character.  When generating the outbound X12 message, all instances of separator characters in the payload data are replaced with the specified character. </li><li>**Segment Terminator** – Enter a single character to indicate the end of an EDI segment. </li><li>**Suffix** – Select the character that is used with the segment identifier. If you designate a suffix, then the segment terminator data element can be empty. If the segment terminator is left empty, then you must designate a suffix. </li> </ul>|
**Control Numbers**

|||
|-|-|
|Interchange Control Number (ISA13) <br /> <br />|Required. Enter a range of values for the interchange control number used by the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] in generating an outgoing interchange. Enter a numeric value with a minimum of 1 and a maximum of 999999999. <br /> <br />|
|Group Control Number (GS06) <br /> <br />|Required. Enter the range of numbers that the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] should use for the group control number. Enter a numeric value with a minimum of one character and a maximum of nine characters. <br /> <br />|
|Transaction Set Control Number (ST02) <br /> <br />|For Transaction Set Control number (ST02), enter a range of numeric values for the required middle fields, and alphanumeric values for the optional prefix and suffix. The maximum length of all four fields is nine characters. <br /> <br />|
|Prefix <br /> <br />|To designate the range of transaction set control numbers used in an acknowledgment, enter values in the ACK Control number (ST02) fields. Enter a numeric value for the middle two fields, and an alphanumeric value (if desired) for the prefix and suffix fields. The middle fields are required and contain the minimum and maximum values for the control number; the prefix and suffix are optional. The maximum length for all three fields is nine characters. <br /> <br />|
|Suffix <br /> <br />|To designate the range of transaction set control numbers used in an acknowledgment, enter values in the ACK Control number (ST02) fields. Enter a numeric value for the middle two fields, and an alphanumeric value (if desired) for the prefix and suffix fields. The middle fields are required and contain the minimum and maximum values for the control number; the prefix and suffix are optional. The maximum length for all three fields is nine characters. <br /> <br />|
**Validation**

|||
|-|-|
|EDI Validation <br /> <br />|Selecting this option enables validation on the interchange receiver. This validation performs EDI validation on transaction-set data elements, validating data types, length restrictions, and empty data elements and training separators. <br /> <br />|
|Extended Validation <br /> <br />|Selecting this option enables extended validation of interchanges received from the interchange sender. This includes validation of field length, optionality, and repeat count in addition to XSD data type validation. You can enable extension validation without enabling EDI validation, or vice versa. <br /> <br />|
|Allow leading/ trailing zeroes <br /> <br />|Selecting this option specifies that an EDI interchange received from the party does not fail validation if a data element in an EDI interchange does not conform to its length requirement because of or trailing spaces, but does conform to its length requirement when they are removed. <br /> <br />|
|Trailing separator <br /> <br />|Selecting this option specifies an EDI interchange received from the party does not fail validation if a data element in an EDI interchange does not conform to its length requirement because of leading (or trailing) zeroes or trailing spaces, but does conform to its length requirement when they are removed. <br /> <br /><ul><li>Select Not Allowed if you do not want to allow trailing delimiters and separators in an interchange received from the interchange sender. If the interchange contains trailing delimiters and separators, it is declared invalid. </li><li>Select Optional to accept interchanges with or without trailing delimiters and separators. </li><li>Select Mandatory if the received interchange must contain trailing delimiters and separators. </li> </ul>|
Select **Save** to save the agreement.

## Known Issue
The [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] allows you to modify the Qualifier of an Identity when an agreement is configured. This can result in inconsistence properties. For example, there is an agreement using ZZ:1234567 and ZZ:7654321 as the Qualifier. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] profile settings, you change ZZ:1234567 to be 01:*ChangedValue*. You open the agreement and 01:*ChangedValue* is displayed instead of ZZ:1234567.

To modify the Qualifier of an identity, delete the agreement, update **Identities** in the partner profile, and then recreate the agreement.

## See Also
[Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md)

