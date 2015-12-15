---
description: na
keywords: na
pagetitle: Configuring Agreements from a BizTalk perspective
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ba64033-e9d8-472f-a00f-261b540ac96f
---
# Configuring Agreements from a BizTalk perspective
Configuring EDI messaging in the [!INCLUDE[tpm_full](/Token/tpm_full_md.md)] is different when compared with BizTalk Server TPM Portal. Following is an overview of the [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] steps to configuring in the [!INCLUDE[tpm_full](/Token/tpm_full_md.md)]:

1. Log in to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. The first time you log in, you are prompted to register you/your company’s BizTalk Service deployment. You can then add “partners.” [BizTalk Server “Party” and BizTalk Services “Partners”](/Topic/Configuring_Agreements_from_a_BizTalk_perspective.md#BKMK_BTSParty) section discusses these steps.

2. When “partners” are created in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, a profile is automatically created for every partner. You can also create new profiles or update the existing profile. [BizTalk Server “Profile” and BizTalk Services “Profile”](/Topic/Configuring_Agreements_from_a_BizTalk_perspective.md#BKMK_BTSProfile) section discusses this information.

3. Create an X12 or AS2 agreement between the partners. General Settings, Receive Settings, and Send Settings are configured. [BizTalk Server “Agreement” and BizTalk Services “Agreement”](/Topic/Configuring_Agreements_from_a_BizTalk_perspective.md#BKMK_BTSAgreement) section discusses this information.

4. When complete, deploy the agreement. [BizTalk Server “Enable” and BizTalk Services “Deploy](/Topic/Configuring_Agreements_from_a_BizTalk_perspective.md#BKMK_BTSEnable) section discusses this information.

This topic acts as a guide for configuring EDI components in [!INCLUDE[af_integration](/Token/af_integration_md.md)] compared to BizTalk Server.

## <a name="BKMK_BTSParty"></a>BizTalk Server “Party” and BizTalk Services “Partners”
A “party” in BizTalk Server is called a “partner” in [!INCLUDE[af_integration](/Token/af_integration_md.md)]. The following tables compare the “party” settings in BizTalk Server with the “partner” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

### Represent you or your company to send messages or receive messages
This table lists the different tasks involved when registering you or your company’s BizTalk Service deployment. It lists the “party” tasks in BizTalk Server and the replacement “partner” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] <br /> <br />|
|--------|------------------|-----------------------------------------------------------|
|Create the “partner” <br /> <br />|In BizTalk Administration, create a new Party and check **Local BizTalk processes messages received by the party or supports sending messages from this party**. <br /> <br />This option establishes you or your company as the service provider. This is the only time you check this option when creating a party. <br /> <br />[How to Create a Party](http://go.microsoft.com/fwlink/p/?LinkId=247301) provides the details. <br /> <br />|The first time you log in to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], you register you/your company’s BizTalk Service. This is the only time you enter the BizTalk Service. Once configured, the BizTalk Service cannot be deleted. <br /> <br />[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md) provides the details. <br /> <br />|
|Optionally, enter additional details, like your name, phone number, e-mail address, etc. <br /> <br />|In BizTalk Administration, open your party properties and add **Additional Properties**. <br /> <br />[How to Create a Party](http://go.microsoft.com/fwlink/p/?LinkId=247301) provides the details. <br /> <br />|The very first time you log in to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], you register you or your company’s BizTalk Service. You can later add additional details. <br /> <br />[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md) provides the details. <br /> <br />|
|Send <br /> <br />|In BizTalk Administration, open your party properties and select **Send Ports**. This associates the send port(s) with your service provider party. <br /> <br />[How to Create a Party](http://go.microsoft.com/fwlink/p/?LinkId=247301) provides the details. <br /> <br />|The “send” is configured when an agreement is created between two partners. Specifically: <br /> <br /><ol><li>Create the partners using [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md). </li><li>Create an agreement between the partners using [Create Agreements in Azure BizTalk Services](/Topic/Create_Agreements_in_Azure_BizTalk_Services.md). </li><li>Configure the send settings using X12 Send Settings ([Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md)) and AS2 Send Settings ([Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md)). </li> </ol>|
|Certificate <br /> <br />|In BizTalk Administration, open your party properties and select **Certificate**. <br /> <br />[How to Create a Party](http://go.microsoft.com/fwlink/p/?LinkId=247301) provides the details. <br /> <br />|The certificate is associated with you or your company’s profile. <br /> <br />When a partner is created, a profile is automatically created. A certificate can then be added to the profile. Specifically: <br /> <br /><ol><li>Create a partner. </li><li>Add a profile. </li><li>Add a certificate to the profile. </li> </ol>See [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md). <br /> <br />|
To summarize:

- To add you or your company as a service provider in BizTalk Server, create a party and check the **Local BizTalk processes messages received by the party or supports sending messages from this party** option in the party properties. See [How to Create a Party](http://go.microsoft.com/fwlink/?LinkId=247301).

- To register you or your company’s BizTalk Service, log in to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] for the very first time and enter your properties. See [Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md).

### Add “partners”
This table lists the task involved when creating a partner. It lists the “party” task in BizTalk Server and the replacement “partner” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] <br /> <br />|
|--------|------------------|-----------------------------------------------------------|
|Create the “partner” <br /> <br />|In BizTalk Administration, create a new Party. Do NOT check **Local BizTalk processes messages received by the party or supports sending messages from this party**. <br /> <br />[How to Create a Party](http://go.microsoft.com/fwlink/p/?LinkId=247301) provides the details. <br /> <br />|In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Partners**. [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md) provides the steps. <br /> <br />|
To summarize on how to create a “partner”:

- In BizTalk Server, create a “party.” Do **NOT** check the **Local BizTalk processes messages received by the party or supports sending messages from this party** option in the party properties. See [How to Create a Party](http://go.microsoft.com/fwlink/p/?LinkId=247301).

- In [!INCLUDE[af_integration](/Token/af_integration_md.md)], create a “partner.” See [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md).

## <a name="BKMK_BTSProfile"></a>BizTalk Server “Profile” and BizTalk Services “Profile”
“Profiles” exist in BizTalk Server and [!INCLUDE[af_integration](/Token/af_integration_md.md)]. The following table compares the “profile” settings in BizTalk Server with the “profile” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

### Add a profile
This table lists the task involved to add or edit a profile. It lists the “profile” tasks in BizTalk Server and the replacement “profile” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] <br /> <br />|
|--------|------------------|-----------------------------------------------------------|
|Create/edit a profile. <br /> <br />|When a party is created in BizTalk Administration, a profile is automatically created. The profile properties include: <br /> <br /><ul><li>General: Includes Name, Description, and Additional Properties. </li><li>Identities: Includes an identity qualifier, like Mutually Defined ZZ. </li> </ul>[Configuring Business Profile Properties](http://go.microsoft.com/fwlink/p/?LinkId=247331) provides the steps to add/edit a party profile. <br /> <br />|When a partner is created in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)], a profile is automatically created. Click the partner name to edit similar properties: <br /> <br /><ul><li>Profile name </li><li>Description </li><li>Identities </li><li>Certificates </li><li>Templates </li> </ul>[Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md) provides the steps to add and edit a partner profile. <br /> <br />|
To summarize on how to create a profile:

- When a party is created in BizTalk Server, a profile is automatically created. This profile can be modified. See [Managing Business Profiles](http://go.microsoft.com/fwlink/?LinkId=247615).

- When a party is created in [!INCLUDE[af_integration](/Token/af_integration_md.md)], a profile is automatically created. This profile can be modified. To start configuring profiles, see [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md).

## <a name="BKMK_BTSAgreement"></a>BizTalk Server “Agreement” and BizTalk Services “Agreement”
“Agreements” exist in BizTalk Server and [!INCLUDE[af_integration](/Token/af_integration_md.md)]. The following tables compare the “agreement” settings in BizTalk Server with the “agreement” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

### X12 Agreements

#### Add an Agreement: X12 General settings
This table lists the different tasks involved when adding an agreement and configuring “General” settings. It lists the “agreement” tasks in BizTalk Server and the replacement “agreement” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] <br /> <br />|
|--------|------------------|-----------------------------------------------------------|
|Create an agreement: General <br /> <br />|A profile is required to create an agreement. In BizTalk Administration, right-click the profile and create a new agreement. This option displays the following properties: <br /> <br /><ul><li>General Properties: Includes the agreement name, the X12 protocol, the First Party, the Second Party, enabling the agreement and logging. </li><li>Contact Information: The contact details. </li><li>Additional Properties: Include any name-value pair. </li> </ul>[Configuring General Settings (X12)](http://go.microsoft.com/fwlink/p/?LinkId=247459) provides the steps to edit these properties. <br /> <br />No identifiers are configured in the General properties in BizTalk Server. <br /> <br />|A profile is required to create an agreement. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Agreements** and then click the **X12** tab. The General tab is opened and displays the following properties: <br /> <br /><ul><li>Agreement name </li><li>Agreement Description </li><li>Hosted Partner </li><li>Hosted Partner Qualifier and Value (ISA5 and ISA6). <br /> <br />   In BizTalk Server, ISA5 and ISA6 are configured in the agreement receive and send properties. </li><li>Guest Partner </li><li>Guest Partner Qualifier and Value (ISA5 and ISA6). <br /> <br />   In BizTalk Server, ISA5 and ISA6 are configured in the agreement receive and send properties. </li><li>Track Send side message properties <br /> <br />   In BizTalk Server, errors can be logged when EDI reporting is enabled. </li><li>Track Receive side message properties <br /> <br />   In BizTalk Server, errors can be logged when EDI reporting is enabled. </li> </ul>See [Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md). <br /> <br />|
To summarize on how to create an agreement:

- When an agreement is created in BizTalk Server, configure the **General** settings. See [Configuring General Settings (X12)](http://go.microsoft.com/fwlink/p/?LinkId=247459).

- When an agreement is created in [!INCLUDE[af_integration](/Token/af_integration_md.md)], configure the **General Settings**. See [Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md).

#### Add an Agreement: X12 Receive settings
> [!WARNING]
> If you click another tab while creating the agreement, the agreement settings are not saved.

This table lists the different tasks involved when adding an agreement and configuring “Receive” settings. It lists the “agreement” tasks in BizTalk Server and the replacement “agreement” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server setting <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] replacement <br /> <br />|
|--------|--------------------------|-----------------------------------------------------------------------|
|Receive Properties Location <br /> <br />|When you click OK in the Agreement General Properties, two new tabs display: **First Party-&gt;Second Party** and **Second Party-&gt;First Party**. <br /> <br />The **Second Party-&gt;First Party** is the Receive. **Important:** In this scenario, First Party is the Service Provider; which means **Local BizTalk processes messages received by the party or supports sending messages from this party** is enabled for the First Party. <br />|In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Agreements**, click the **X12** tab, and then **Create Agreement**. The General Settings are opened, which are previously described. When the General Settings are added, click **Continue** to display the Receive properties. **Important:** This agreement in BizTalk Server translate to two separate agreements in [!INCLUDE[af_integration](/Token/af_integration_md.md)]:**Agreement 1**: First Party is the Hosted Partner.**Agreement 2**: Second Party is the Hosted Partner. <br />|
**Interchange Settings**

|Task <br /> <br />|BizTalk Server setting <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] replacement <br /> <br />|
|--------|--------------------------|-----------------------------------------------------------------------|
|Identifiers <br /> <br />|<ul><li>Authorization qualifier (ISA1) </li><li>Value (ISA2) </li><li>Security qualifier (ISA3) </li><li>Value (ISA4) </li><li>Sender Id Qualifier (ISA5) </li><li>Value (ISA6) </li><li>Receiver Id Qualifier </li><li>Value (ISA8) </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>Authorization qualifier (ISA1) </li><li>ISA2 </li><li>Security qualifier (ISA3) </li><li>ISA4 </li> </ul>The **X12 General Settings** have the equivalent settings: <br /> <br /><ul><li>Hosted Partner Qualifier (ISA5) </li><li>Hosted Partner Value (ISA6) </li><li>Guest Partner Qualifier (ISA7) </li><li>Guest Partner Value (ISA8) </li> </ul> **Note:** In BizTalk Server, the receive agreement and send agreement can have a different pair of sender and receiver identities (ISA 5, ISA6, ISA7, ISA8). In [!INCLUDE[af_integration](/Token/af_integration_md.md)], the identity pair is the same for receive and send agreements. <br />|
|Acknowledgements <br /> <br />|<ul><li>TA1 Expected </li><li>997 Expected </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>TA1 Expected: Returns technical (TA1) acknowledgment to the interchange sender (based on the Send Settings for the agreement). </li><li>997 Expected: Returns functional (997) acknowledgment to the interchange sender (based on the Send Settings for the agreement). </li> </ul>|
|Envelopes <br /> <br />|Configured in Send. <br /> <br />|No equivalent configuration. <br /> <br />|
|Character set and separators <br /> <br />|Character set to be used: Basic, Extended, or UTF8/Unicode. <br /> <br />|No equivalent configuration. <br /> <br />|
|Local Host Settings <br /> <br />|<ul><li>ACK control numbers (STO2) </li><li>Reset to lower limit when out of bound </li><li>Route ACK to send pipeline on request-response receive port </li><li>Mask security/authorization/password information in context property </li><li>Inbound batch processing option </li> </ul>|No equivalent configuration. <br /> <br />|
|Validation <br /> <br />|<ul><li>Interchange Control Number <br /> <br />   Check for duplicate ISA13 within the following number of days </li><li>Group Control Number </li><li>Transaction Set Control Number </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>Interchange Control Number <br /> <br />   Check for duplicate ISA13 every days </li><li>Group control number </li><li>Transaction set control number </li> </ul>|
|Batch Configuration <br /> <br />|Configured in Send. <br /> <br />|No equivalent configuration. <br /> <br />|
|Send Ports <br /> <br />|Configured in Send. <br /> <br />|No equivalent configuration. <br /> <br />|
**Transaction Set Settings**

|Task <br /> <br />|BizTalk Server setting <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] replacement <br /> <br />|
|--------|--------------------------|-----------------------------------------------------------------------|
|Transaction Set List <br /> <br />|<ul><li>Support Transaction Sets from the List </li><li>Exclude Transaction Sets from the List </li> </ul>|No equivalent configuration. On the other hand, the equivalent is implicit because only the message types configured in the X12 Agreement (Receive Settings, Schemas) are allowed. Messages corresponding to other message types are suspended. <br /> <br />|
|Validation <br /> <br />|<ul><li>Default </li><li>Transaction Type </li><li>Edi Type Validation </li><li>Extended Validation </li><li>Allow Leading &amp; Trailing Spaces &amp; Zeroes </li><li>Trailing Separators </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>Split Interchange as Transaction sets: Equivalent to checking **Default** check box in BizTalk Server. </li><li>Preserve Interchange: Equivalent to not checking **Default** check box in BizTalk Server. </li> </ul>Advanced Settings (Validation) in the **Protocol** page has the following equivalent settings: <br /> <br /><ul><li>Transaction Type </li><li>Edi Type Validation </li><li>Extended Validation </li><li>Allow Leading &amp; Trailing Spaces &amp; Zeroes </li><li>Trailing Separators </li> </ul>|
|Local Host Settings <br /> <br />|<ul><li>Convert implied decimal format Nn to base 10 numeric value </li><li>Create empty XML tags if trailing separators are allowed </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>Convert implied decimal format Nn to base 10 numeric value </li><li>Create empty XML tags if trailing separators are allowed </li> </ul>|
|Envelopes <br /> <br />|Configured in Send. <br /> <br />|No equivalent configuration. <br /> <br />|
To summarize on how to add X12 Receive settings:

- When an agreement is created in BizTalk Server, configure the **General** settings and then configure the Receive settings. See [Configuring Interchange Settings (X12)](http://go.microsoft.com/fwlink/p/?LinkId=247467) and [Configuring Transaction Set Settings (X12)](http://go.microsoft.com/fwlink/p/?LinkId=247468).

- When an agreement is created in [!INCLUDE[af_integration](/Token/af_integration_md.md)], configure the **General Settings** and then configure the **Receive Settings**. See [Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md).

#### Add an Agreement: X12 Send settings
> [!WARNING]
> If you click another tab while creating the agreement, the agreement settings are not saved.

This table lists the different tasks involved when adding an agreement and configuring “Send” settings. It lists the “agreement” tasks in BizTalk Server and the replacement “agreement” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server setting <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] replacement <br /> <br />|
|--------|--------------------------|-----------------------------------------------------------------------|
|Send Properties Location <br /> <br />|When you click OK in the Agreement General Properties, two new tabs display: **First Party-&gt;Second Party** and **Second Party-&gt;First Party**. <br /> <br />The **First Party-&gt;Second Party** is the Send. <br /> <br />|In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Agreements**, click the X12 tab, and then click **Create Agreement**. The General Settings are opened, which are previously described. When the General Settings are added, click **Continue** and then click the Send tab to display the Send properties. <br /> <br />|
**Interchange Settings**

|Task <br /> <br />|BizTalk Server setting <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] replacement <br /> <br />|
|--------|--------------------------|-----------------------------------------------------------------------|
|Identifiers <br /> <br />|<ul><li>Authorization qualifier (ISA1) </li><li>Value (ISA2) </li><li>Security qualifier (ISA3) </li><li>Value (ISA4) </li><li>Sender Id Qualifier (ISA5) </li><li>Value (ISA6) </li><li>Receiver Id Qualifier (ISA7) </li><li>Value (ISA8) </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>Authorization qualifier (ISA1) </li><li>ISA2 </li><li>Security qualifier (ISA3) </li><li>ISA4 </li> </ul>No equivalent configuration for the following BizTalk Server settings: <br /> <br /><ul><li>Sender Id Qualifier (ISA5) </li><li>Value (ISA6) </li><li>Receiver Id Qualifier (ISA7) </li><li>Value (ISA8) </li> </ul>|
|Acknowledgements <br /> <br />|<ul><li>TA1 Expected </li><li>997 Expected </li><li>Include AK2 loop for accepted transaction sets </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>TA1 Expected: Returns technical (TA1) acknowledgment to the interchange sender (based on the Send Settings for the agreement). </li><li>997 Expected: Returns functional (997) acknowledgment to the interchange sender (based on the Send Settings for the agreement). </li><li>Include AK2 Loop </li> </ul>|
|Envelopes <br /> <br />|<ul><li>ISA11 Usage: Choose Standard identifier or Repetition separator </li><li>Control version number (ISA12) </li><li>Usage indicator (ISA15) </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>ISA11 Usage: Choose Standard identifier or Repetition separator </li><li>Control Version Number (ISA12) </li><li>Usage Indicator </li> </ul>In BizTalk Server, you select the transaction type. In [!INCLUDE[af_integration](/Token/af_integration_md.md)], you select the schema for which these envelope settings should be applied. <br /> <br />|
|Character set and separators <br /> <br />|<ul><li>Character set to be used </li><li>Data element </li><li>Component element separator (ISA16) </li><li>Segment terminator </li><li>Suffix: None, CR, LF, CR LF </li><li>Replace separators in payload with </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>Character Set to be used </li><li>Data Element Separator </li><li>Component element separator </li><li>Segment Terminator </li><li>Suffix </li><li>Replace separators in payload with </li> </ul>|
|Local Host Settings <br /> <br />|<ul><li>Interchange Control Number (ISA13) </li><li>Group Control Number (GS06) </li><li>Transaction Set Control Number (ST02) </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>Interchange Control Number (ISA13) </li><li>Group Control Number (GS06) </li><li>Transaction Set Control Number (ST02) </li><li>Prefix: Equivalent to the starting number. </li><li>Suffix: Equivalent to the ending number. </li> </ul>|
|Validation <br /> <br />|<ul><li>Interchange Control Number <br /> <br />   Check for duplicate ISA13 within the following number of days </li><li>Group Control Number </li><li>Transaction Set Control Number </li> </ul>|No equivalent configuration. <br /> <br />|
|Batch Configuration <br /> <br />|New Batch: <br /> <br /><ul><li>Identification: Batch name and Batch description </li><li>Filter </li><li>Release: Schedule, Maximum number of transactions sets in, Maximum number of characters in an interchange and External release trigger </li><li>Activation: Start immediately </li><li>Termination: No end date, End after and End by </li> </ul>|The **Batching** page has the equivalent settings: <br /> <br /><ul><li>Name </li><li>Description </li><li>Count: Similar to Release. </li><li>Deploy: Equivalent to Activation. When the Agreement is deployed, the Batch is started. </li><li>Delete Batch: Equivalent to Termination. When a Batch is deleted and the Agreement is redeployed, the Batch is removed. </li> </ul>|
|Send Ports <br /> <br />|Send ports <br /> <br />|The **Transport** page has the equivalent settings, which include sending the message to [!INCLUDE[sb2](/Token/sb2_md.md)], [!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)], [!INCLUDE[azure_1](/Token/azure_1_md.md)] blob destinations, an HTTP URL, an FTP server or an AS2 transport. <br /> <br />|
**Transaction Set Settings**

|Task <br /> <br />|BizTalk Server setting <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] replacement <br /> <br />|
|--------|--------------------------|-----------------------------------------------------------------------|
|Transaction Set List <br /> <br />|<ul><li>Support Transaction Sets from the List </li><li>Exclude Transaction Sets from the List </li> </ul>|No equivalent configuration. On the other hand, the equivalent is implicit because only the message types configured in the X12 Agreement (Send Settings, Schemas) are allowed. Messages corresponding to other message types are suspended. <br /> <br />|
|Validation <br /> <br />|<ul><li>Default </li><li>Transaction Type </li><li>Edi Type Validation </li><li>Extended Validation </li><li>Allow Leading &amp; Trailing Spaces &amp; Zeroes </li><li>Trailing Separators </li> </ul>|The **Protocol** page has the equivalent settings: <br /> <br /><ul><li>EDI Validation: Equivalent to **Edi Type Validation** in BizTalk Server. </li><li>Extended Validation </li><li>Allow leading/trailing zeroes </li><li>Trailing separator </li> </ul>No equivalent configuration for the following BizTalk Server settings: <br /> <br /><ul><li>Default </li><li>Transaction Type </li><li>Default </li> </ul>|
|Local Host Settings <br /> <br />|Configured in Receive. <br /> <br />|No equivalent configuration. <br /> <br />|
|Envelopes <br /> <br />|<ul><li>Default </li><li>Transaction Type </li><li>Version/Release </li><li>Target namespace </li><li>GS1 </li><li>GS2 </li><li>GS3 </li><li>GS4 </li><li>GS5 </li><li>GS6 </li><li>GS7 </li><li>GS8 </li> </ul>|The **Protocol** page has the equivalent Schemas option. <br /> <br />|
To summarize on how to add X12 Send settings:

- When an agreement is created in BizTalk Server, configure the **General** settings, configure the Receive settings, and then configure the Send settings. See [Configuring Interchange Settings (X12)](http://go.microsoft.com/fwlink/p/?LinkId=247467) and [Configuring Transaction Set Settings (X12)](http://go.microsoft.com/fwlink/p/?LinkId=247468).

- When an agreement is created in [!INCLUDE[af_integration](/Token/af_integration_md.md)], configure the **General Settings**, configure the **Receive Settings**, and then configure the **Send Settings**. See [Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md).

### AS2 Agreements

#### Add an Agreement: AS2 General settings
This table lists the different tasks involved when adding an agreement and configuring “General” settings. It lists the “agreement” tasks in BizTalk Server and the replacement “agreement” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] <br /> <br />|
|--------|------------------|-----------------------------------------------------------|
|Create an agreement: General <br /> <br />|A profile is required to create an agreement. In BizTalk Administration, right-click the profile and create a new agreement. This option displays the following properties: <br /> <br /><ul><li>General Properties: Includes the agreement name, the AS2 protocol, the First Party, the Second Party, enabling the agreement and logging. </li><li>Contact Information: The contact details. </li><li>Additional Properties: Include any name-value pair. </li> </ul>[Configuring General Party Properties (AS2)](http://go.microsoft.com/fwlink/p/?LinkId=247461) provide the steps to edit these properties. <br /> <br />No identifiers are configured in the General properties in BizTalk Server. <br /> <br />|A profile is required to create an agreement. In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Agreements** and then click the **AS2** tab. The General tab is opened and displays the following properties: <br /> <br /><ul><li>Agreement name </li><li>Agreement Description </li><li>Hosted Partner: Equivalent to First Party. <br /> <br />   AS2 Identity: Equivalent to **AS2-From** and **AS2-To** in BizTalk Server. </li><li>Hosted Partner Qualifier and Value. </li><li>Guest Partner: Equivalent to Second Party. <br /> <br />   AS2 Identity: AS2 Identity: Equivalent to **AS2-From** and **AS2-To** in BizTalk Server. </li><li>Guest Partner Qualifier and Value. </li><li>Track Send side message properties <br /> <br />   In BizTalk Server, errors can be logged when EDI reporting is enabled. </li><li>Track Receive side message properties <br /> <br />   In BizTalk Server, errors can be logged when EDI reporting is enabled. </li> </ul>See [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md). <br /> <br />|
To summarize on how to add AS2 General settings:

- When an agreement is created in BizTalk Server, configure the **General** settings. See [Configuring General Party Properties (AS2)](http://go.microsoft.com/fwlink/p/?LinkId=247461).

- When an agreement is created in [!INCLUDE[af_integration](/Token/af_integration_md.md)], configure the **General Settings**. See [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md).

#### Add an agreement: AS2 Receive settings
> [!WARNING]
> If you click another tab while creating the agreement, the agreement settings are not saved.

This table lists the different tasks involved when adding an agreement and configuring “Receive” settings. It lists the “agreement” tasks in BizTalk Server and the replacement “agreement” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server setting <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] replacement <br /> <br />|
|--------|--------------------------|-----------------------------------------------------------------------|
|Receive Properties Location <br /> <br />|When you click OK in the Agreement General Properties, two new tabs display: **First Party-&gt;Second Party** and **Second Party-&gt;First Party**. <br /> <br />The **Second Party-&gt;First Party** is the Receive. <br /> <br />|In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Agreements**, click the **AS2** tab, and then **Create Agreement**. The General Settings are opened, which are previously described. When the General Settings are added, click **Continue** to display the Receive properties. <br /> <br />|
|Identifiers <br /> <br />|<ul><li>AS2-From </li><li>AS2-To </li> </ul>|Equivalent to **AS2 Identity** in the **General Settings**. <br /> <br />|
|Validation <br /> <br />|<ul><li>Use agreement settings for validation and MDN instead of message header </li><li>Message should be signed </li><li>Message should be compressed </li><li>Message should be encrypted </li><li>Check Certification Revocation List on receipt of message </li><li>Check for duplicate messages within the following number of days </li> </ul>|Following are the equivalent configuration settings: <br /> <br /><ul><li>Override receive side agreement settings with those in the incoming AS2 message </li><li>Message should be signed </li><li>Message should be compressed under </li><li>Message should be encrypted </li> </ul>No equivalent configuration for the following BizTalk Server settings: <br /> <br /><ul><li>Check Revocation List </li><li>Check for duplicate messages </li> </ul>|
|Acknowledgements (MDNs) <br /> <br />|In BizTalk Server, the following acknowledgment options are telling the sending party to include the MDN. Another way of saying this is that receiving party is “requesting” the MDN. <br /> <br /><ul><li>Process inbound MDN into MessageBox for routing/delivery options </li><li>Request MDN </li><li>Request signed MDN </li><li>Request asynchronous MDN, including the Receipt-Delivery Option URL </li><li>Receipt-Delivery Option URL </li><li>Resend AS2 message if MDN not received </li><li>Override send port settings </li><li>Disposition-Notification-To </li> </ul>|In [!INCLUDE[af_integration](/Token/af_integration_md.md)], acknowledgment messages are sent from the managed partner to the unmanaged partner (based on the Transport URL in the Send Settings). MDN options include: <br /> <br /><ul><li>MDN Text </li><li>Send MDN </li><li>Send signed MDN </li><li>Send asynchronous MDN </li><li>Receive URL Settings, which includes the URL scheme (HTTP or HTTPS) and the URL Suffix. This option is equivalent to the **Receipt-Delivery Option URL** in BizTalk Server. </li> </ul>No equivalent configuration for the following BizTalk Server settings: <br /> <br /><ul><li>Process inbound MDN into MessageBox for routing/delivery options </li><li>Resend AS2 message if MDN not received </li><li>Override send port settings </li><li>Disposition-Notification-To </li> </ul>|
|Local Host Settings <br /> <br />|<ul><li>General </li><li>Receiver MDN Settings </li><li>HTTP Settings for Messages </li><li>HTTP Settings for MDNs </li><li>Sender Message Tracking(NRR) </li><li>Receiver Message Tracking(NRR) </li> </ul>|No equivalent configuration. Tracking is enabled at the General Settings. <br /> <br />|
|Signature Certificate <br /> <br />|<ul><li>Override group signing certificate </li> </ul>|No equivalent configuration. Certificates are added when a partner is configured. See [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md). <br /> <br />|
|Send Ports <br /> <br />|Configured in Send. <br /> <br />|In the **Route Settings** tab, you can route to the following: <br /> <br /><ul><li>[!INCLUDE[af_integration](/Token/af_integration_md.md)][!INCLUDE[bridge](/Token/bridge_md.md)] </li><li>[!INCLUDE[azure_1](/Token/azure_1_md.md)] blob </li><li>[!INCLUDE[sb2](/Token/sb2_md.md)] </li> </ul>|
To summarize on how to add AS2 Receive settings:

- When an agreement is created in BizTalk Server, configure the **General** settings and then configure the Receive settings. See [Configuring AS2 Agreement Properties](http://go.microsoft.com/fwlink/p/?LinkId=247466).

- When an agreement is created in [!INCLUDE[af_integration](/Token/af_integration_md.md)], configure the **General Settings** and then configure the **Receive Settings**. See [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md).

#### Add an agreement: AS2 Send settings
> [!WARNING]
> If you click another tab while creating the agreement, the agreement settings are not saved.

This table lists the different tasks involved when adding an agreement and configuring “Send” settings. It lists the “agreement” tasks in BizTalk Server and the replacement “agreement” settings in [!INCLUDE[af_integration](/Token/af_integration_md.md)].

|Task <br /> <br />|BizTalk Server setting <br /> <br />|[!INCLUDE[af_integration](/Token/af_integration_md.md)] replacement <br /> <br />|
|--------|--------------------------|-----------------------------------------------------------------------|
|Send Properties Location <br /> <br />|When you click OK in the Agreement General Properties, two new tabs display: **First Party-&gt;Second Party** and **Second Party-&gt;First Party**. <br /> <br />The **First Party-&gt;Second Party** is the Send. <br /> <br />|In the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page, click **Agreements**, click the AS2 tab, and then click **Create Agreement**. The General Settings are opened, which are previously described. When the General Settings are added, click **Continue** and then click the Send tab to display the Send properties. <br /> <br />|
|Identifiers <br /> <br />|<ul><li>AS2-From </li><li>AS2-To </li> </ul>|Equivalent to **AS2 Identity** in the **General Settings**. <br /> <br />|
|Validation <br /> <br />|<ul><li>Message should be signed </li><li>Message should be compressed </li><li>Message should be encrypted </li><li>Check Certification Revocation List on receipt of message </li><li>Check for duplicate messages within the following number of days </li> </ul>|Following are the equivalent configuration settings: <br /> <br /><ul><li>Enable Message signing </li><li>Enable message encryption </li><li>Enable message compression </li> </ul>No equivalent configuration for the following BizTalk Server settings: <br /> <br /><ul><li>Check Revocation List </li><li>Check for duplicate messages </li> </ul>|
|Acknowledgements (MDNs) <br /> <br />|In BizTalk Server, the following acknowledgment options are telling the sending party to include the MDN. Another way of saying this is that receiving party is “requesting” the MDN. <br /> <br /><ul><li>Process inbound MDN into MessageBox for routing/delivery options </li><li>Request MDN </li><li>Request signed MDN </li><li>Request asynchronous MDN </li><li>Receipt-Delivery Option URL </li><li>Resend AS2 message if MDN not received </li><li>Override send port settings </li><li>Disposition-Notification-To </li> </ul>|In [!INCLUDE[af_integration](/Token/af_integration_md.md)], this setting configures the agreement to send MDN receipts to the sender on the original AS2 message after the message has been delivered. MDN options include: <br /> <br /><ul><li>Request MDN </li><li>Request signed MDN </li><li>Request asynchronous MDN </li><li>Transport Settings: This option is equivalent to the **Receipt-Delivery Option URL** in BizTalk Server. </li> </ul>No equivalent configuration for the following BizTalk Server settings: <br /> <br /><ul><li>Process inbound MDN into MessageBox for routing/delivery options </li><li>Resend AS2 message if MDN not received </li><li>Override send port settings </li><li>Disposition-Notification-To </li> </ul>|
|Local Host Settings <br /> <br />|<ul><li>General </li><li>Receiver MDN Settings </li><li>HTTP Settings for Messages </li><li>HTTP Settings for MDNs </li><li>Sender Message Tracking(NRR) </li><li>Receiver Message Tracking(NRR) </li> </ul>|No equivalent configuration. Tracking is enabled at the General Settings. <br /> <br />|
|Signature Certificate <br /> <br />|<ul><li>Override group signing certificate </li> </ul>|No equivalent configuration. Certificates are added when a partner is configured. See [Manage Partners and Profiles in Azure BizTalk Services](/Topic/Manage_Partners_and_Profiles_in_Azure_BizTalk_Services.md). <br /> <br />|
|Send Ports <br /> <br />|Send ports <br /> <br />|No equivalent configuration. <br /> <br />|
To summarize on how to add AS2 Send settings:

- When an agreement is created in BizTalk Server, configure the **General** settings, configure the Receive settings, and then configure the Send settings. See [Configuring AS2 Agreement Properties](http://go.microsoft.com/fwlink/p/?LinkId=247466).

- When an agreement is created in [!INCLUDE[af_integration](/Token/af_integration_md.md)], configure the **General Settings**, configure the **Receive Settings**, and then configure the **Send Settings**. See [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md).

Summary Overview:

- In BizTalk Server, an agreement has **General Settings**, **Second Party-&gt;First Party** (Receive) settings and **First Party-&gt;Second Party** (Send) settings. Each settings section is separated by tabs when creating an agreement in BizTalk Administration. See [Managing Agreements](http://go.microsoft.com/fwlink/p/?LinkId=247616).

- In [!INCLUDE[af_integration](/Token/af_integration_md.md)], an agreement has **General Settings**, **Receive Settings** and **Send Settings**. Each settings section is separated by tabs when creating an agreement in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)]. See [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md) and [Create an X12 Agreement in Azure BizTalk Services](/Topic/Create_an_X12_Agreement_in_Azure_BizTalk_Services.md).

## <a name="BKMK_BTSEnable"></a>BizTalk Server “Enable” and BizTalk Services “Deploy
In BizTalk Server, when an Agreement is configured, you **Enable** the agreement in BizTalk Administration by right-clicking the Agreement and clicking **Enable**. In [!INCLUDE[af_integration](/Token/af_integration_md.md)] when the Agreement is configured, you **Deploy** the agreement in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] home page by clicking **Deploy**.

To summarize deploying the agreement:

- In BizTalk Server, you **Enable** an agreement in BizTalk Administration. See [How to Enable or Disable an Agreement](http://go.microsoft.com/fwlink/?LinkId=247617).

- In [!INCLUDE[af_integration](/Token/af_integration_md.md)], you **Deploy** an agreement in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)].

## See Also
[Configuring EDI, AS2, and EDIFACT on BizTalk Services Portal](/Topic/Configuring_EDI,_AS2,_and_EDIFACT_on_BizTalk_Services_Portal.md)
[EDI, AS2, and EDIFACT Messaging &#40;Business to Business&#41;](/Topic/EDI,_AS2,_and_EDIFACT_Messaging__Business_to_Business).md)

