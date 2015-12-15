---
description: na
keywords: na
pagetitle: Example: Creating an AS2 Agreement in BizTalk Services Using the TPM OM API
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 932cea59-2623-4626-9945-127cc3a5d3e2
---
# Example: Creating an AS2 Agreement in BizTalk Services Using the TPM OM API
Example: How to create an AS2 agreement using the TPM OM API with C#.

### To create an AS2 agreement using C#

1. Create a Visual Studio C# project and in your Program.cs file, and follow the instructions under the [The First Steps](/Topic/Creating_.NET_Applications_Using_TPM_OM_REST_API.md#BKMK_FirstSteps) section. Remember to include the service reference to the WCF Data Services client library that you created by adding a service reference to the TPM OM REST API. For example:

   ```unstlib
   using BtsServices.PartnerManagement;
   ```
   Here, **BtsServices** is the name of your C# project in Visual Studio and **PartnerManagement** is the name of the service reference to the TPM OM REST endpoint.

2. Add reference to the following namespaces:

   ```c#
   using System.Collections.Specialized;
   using System.Data.Services.Client;
   using System.Net;
   using System.Web;
   ```

3. Declare the variables to hold the values that are required by the program. Such as:

   ```c#
   private static string acsAddress = "bts_svc_acs_sample"; //sample ACS URL
   private static string baseUrl = "bts_svc_tpm_metadata"; //sample base URL for TPM OM API
   private static TpmContext context = null;
   private static string issuerKey = "<issuer_key>";
   private static string issuerName = "owner";
   private static string token = string.Empty;
   ```

4. Retrieve the WRAP ACS token to authenticate with the service. You can use any WRAP token to authenticate, however the following code demonstrates how to retrieve a password token. For more information on how to retrieve WRAP ACS token, see [http://msdn.microsoft.com/library/windowsazure/hh674475.aspx](http://msdn.microsoft.com/library/windowsazure/hh674475.aspx).

   ```c#
   private static string GetAcsToken(string acsAddress, string issuerName, string issuerKey, string appliesToAddress)
   {
       using (WebClient client = new WebClient())
       {
           client.BaseAddress = acsAddress;
           NameValueCollection values = new NameValueCollection();
           values.Add("wrap_name", issuerName);
           values.Add("wrap_password", issuerKey);
           values.Add("wrap_scope", appliesToAddress);

           byte[] responseBytes = client.UploadValues("WRAPv0.9/", "POST", values);

           string response = Encoding.UTF8.GetString(responseBytes);

           // Extract the token and return it.
           return response
               .Split('&')
               .Single(value => value.StartsWith("wrap_access_token=", StringComparison.OrdinalIgnoreCase))
               .Split('=')[1];
       }
   }

   private static void GetAcsToken(string address)
   {
       UriBuilder appliesToUriBuilder = new UriBuilder(address);
       appliesToUriBuilder.Scheme = "http";

       if (appliesToUriBuilder.Port == 443)
       {
           appliesToUriBuilder.Port = -1;
       }
       token = GetAcsToken(acsAddress, issuerName, issuerKey, appliesToUriBuilder.Uri.ToString());
   }
   ```

5. Pass the [!INCLUDE[ac2](/Token/ac2_md.md)] tokens as a header to the request message. Also pass the other mandatory header (x-ms-version) with the request message:

   ```c#
   private static void AppendAuthToContext(object sender, SendingRequestEventArgs e)
   {
       var request = (HttpWebRequest)e.Request;
       request.Headers["x-ms-version"] = "1.0"; //For this release, set the value of this header to 1.0
       request.Headers[HttpRequestHeader.Authorization] = "WRAP access_token=\"" +
                                                                    HttpUtility.UrlDecode(token) + "\"";
   }
   ```

6. Define a method in which you bind the TpmContext object created earlier with the service URI for the TPM OM REST endpoint, register the callback method, `AppendAuthToContext`, and set the default save option on the context to batched save:

   ```c#
   private static void Initialize()
   {
       context = new TpmContext(new Uri(baseUrl));
       context.SendingRequest += new EventHandler<SendingRequestEventArgs>(AppendAuthToContext);
       context.SaveChangesDefaultOptions = SaveChangesOptions.Batch; //You must always use batched save for TPM OM API
   }
   ```

7. From the `Main()` function, invoke the `GetAcsToken()` and `Initialize()` functions, and create the first couple of partners:

   ```
   GetAcsToken(baseUrl);
   Initialize();

   string index = "_" + new Random().Next(1000); //a random identifier to append to each partner
                                                 //name to make it unique

   //CREATE FIRST PARTNER
   Partner partnerA = new Partner();
   partnerA.Name = "PartnerA" + index;
   partnerA.Description = "DescriptionA" + index;
   context.AddToPartners(partnerA); //add the newly created partner to the context
   context.SaveChanges(); //save changes to the context.

   //CREATE SECOND PARTNER
   Partner partnerB = new Partner();
   partnerB.Name = "PartnerB" + index;
   partnerB.Description = "DescriptionB" + index;
   context.AddToPartners(partnerB);
   context.SaveChanges();
   ```

8. Create a couple of business profiles and link them to the partners created earlier. To create links between the entities, we typically use the [AddLink](http://msdn.microsoft.com/library/system.data.services.client.dataservicecontext.addlink.aspx) and [SetLink](http://msdn.microsoft.com/library/system.data.services.client.dataservicecontext.setlink.aspx) methods available on the [DataServiceContext](http://msdn.microsoft.com/library/system.data.services.client.dataservicecontext.aspx).

   ```c#
   // CREATE FIRST BUSINESS PROFILE

   BusinessProfile profileA = new BusinessProfile();
   profileA.Name = "ProfileA" + index;
   profileA.Description = "DescriptionA" + index;
   context.AddToBusinessProfiles(profileA);

   //// The BusinessProfile entity has a property 'Partner', which is a type in TpmContext. 
   //// These are navigation properties/links. Some navigation properties/links need 
   //// to be set before we can create this entity. Setting the 'Partner' property is must for
   //// creating BusinessProfile entity.
   context.SetLink(profileA, "Partner", partnerA); //for 1.* or 1.1 links, you must use SetLink
   profileA.Partner = partnerA;

   //// Similarly, for creating a link from a Partner to Business Profile, you must set
   //// the 'BusinessProfiles' navigation property
   context.AddLink(partnerA, "BusinessProfiles", profileA); //for *.* links, you need to use AddLink
   partnerA.BusinessProfiles.Add(profileA);
   context.SaveChanges();

   // CREATE SECOND BUSINESS PROFILE
   BusinessProfile profileB = new BusinessProfile();
   profileB.Name = "ProfileB" + index;
   profileB.Description = "DescriptionB" + index;
   context.AddToBusinessProfiles(profileB);
   context.SetLink(profileB, "Partner", partnerB);
   profileB.Partner = partnerB;
   context.AddLink(partnerB, "BusinessProfiles", profileB);
   partnerB.BusinessProfiles.Add(profileB);
   context.SaveChanges();
   ```

9. Create a couple of business identities and attach them with each business profile. Because BusinessIdentity is an abstract entity, we create a QualifierIdentity that derives from the BusinessIdentity entity.

   ```c#
   // CREATE THE FIRST QUALIFIER IDENTITY
   QualifierIdentity identityA = new QualifierIdentity();
   identityA.Name = "IdentityA" + index;
   identityA.Qualifier = "ZZ";
   identityA.Value = "THEM" + index;
   context.AddToBusinessIdentities(identityA);
   context.SetLink(identityA, "BusinessProfile", profileA);
   identityA.BusinessProfile = profileA;
   context.AddLink(profileA, "BusinessIdentities", identityA);
   profileA.BusinessIdentities.Add(identityA);

   //CREATE THE SECOND QUALIFIER IDENTITY
   QualifierIdentity identityB = new QualifierIdentity();
   identityB.Name = "IdentityB" + index;
   identityB.Qualifier = "ZZ";
   identityB.Value = "US" + index;
   context.AddToBusinessIdentities(identityB);
   context.SetLink(identityB, "BusinessProfile", profileB);
   identityB.BusinessProfile = profileB;
   context.AddLink(profileB, "BusinessIdentities", identityB);
   profileB.BusinessIdentities.Add(identityB);
   context.SaveChanges();
   ```

10. You now create a partnership between the two partners. To create a partnership, you first create a Partnership entity and then link it with the two partners you created earlier:

   ```c#
   // CREATE A PARTNERSHIP
   Partnership partnership = new Partnership();
   context.AddToPartnerships(partnership);

   partnership.PartnerA = partnerA;
   context.SetLink(partnership, "PartnerA", partnerA);
   partnerA.PartnershipsAsA.Add(partnership);
   context.AddLink(partnerA, "PartnershipsAsA", partnership);

   partnership.PartnerB = partnerB;
   context.SetLink(partnership, "PartnerB", partnerB);
   partnerB.PartnershipsAsA.Add(partnership);
   context.AddLink(partnerB, "PartnershipsAsB", partnership);

   context.SaveChanges();
   ```

11. You must now create an agreement between the two partners. As part of the agreement creation process, you must also link it to the business profiles for the two partners, the partnership entity for the two partners, and the one-way agreements (send-side and receive-side). We haven’t created the one-way agreements yet, so in this step we create the agreement and link it to the existing entities, Partnership and BusinessProfile. Because we can’t save changes to the context without linking the agreement to the one-way agreement, we do not save the changes in this step using the `context.SaveChanges()` method.

   ```c#
   //CREATE AN AGREEMENT
   Agreement agreement = new Agreement();
   agreement.Name = "Agreement" + index;
   agreement.ProtocolName = "AS2";
   context.AddToAgreements(agreement);

   //LINK AGREEMENT TO A PARTNERSHIP
   agreement.Partnership = partnership;
   context.SetLink(agreement, "Partnership", partnership);
   partnership.Agreements.Add(agreement);
   context.AddLink(partnership, "Agreements", agreement);

   //LINK AGREEMENT TO PROFILEA
   agreement.BusinessProfileA = profileA;
   context.SetLink(agreement, "BusinessProfileA", profileA);
   profileA.AgreementsAsA.Add(agreement);
   context.AddLink(profileA, "AgreementsAsA", agreement);

   //LINK AGREEMENT TO PROFILEB
   agreement.BusinessProfileB = profileB;
   context.SetLink(agreement, "BusinessProfileB", profileB);
   profileB.AgreementsAsB.Add(agreement);
   context.AddLink(profileB, "AgreementsAsB", agreement);
   ```

12. The next step is to create one-way agreements from PartnerA to PartnerB and from PartnerB to PartnerA. As part of creating a one-way agreement, you should also link it to the entities Agreement, BusinessIdentity, and ProtocolSettings. We have already created the Agreement and BusinessIdentity entities but we haven’t yet created the ProtocolSettings entity. So, in this step, we only create the one-way agreement entities and link them to the Agreement and BusinessIdentity entities. In the next step, we create the ProtocolSettings entity and link it to the one-way agreement entities.

   > [!NOTE]
   > You should not commit the changes to the context before linking the one-way agreement to the ProtocolSettings entity otherwise you would get an exception. Hence, in this step, we do not use the `context.SaveChanges()` method to commit the changes to the context.

   ```c#
   //CREATE ONE-WAY AGREEMENT FROM PARTNER A TO PARTNER B
   OnewayAgreement onewayAgreementAtoB = new OnewayAgreement();
   context.AddToOnewayAgreements(onewayAgreementAtoB);

   //LINK THE ONE-WAY AGREEMENT TO THE AGREEMENT ENTITY
   onewayAgreementAtoB.AgreementAsAToB = agreement;
   context.SetLink(onewayAgreementAtoB, "AgreementAsAToB", agreement);
   agreement.OnewayAgreementAToB = onewayAgreementAtoB;
   context.SetLink(agreement, "OnewayAgreementAToB", onewayAgreementAtoB);

   //LINK THE ONE-WAY AGREEMENT TO BUSINESS IDENTITIES
   onewayAgreementAtoB.SenderBusinessIdentity = identityA;
   context.SetLink(onewayAgreementAtoB, "SenderBusinessIdentity", identityA);
   identityA.OnewayAgreementSender.Add(onewayAgreementAtoB);
   context.AddLink(identityA, "OnewayAgreementSender", onewayAgreementAtoB);
   onewayAgreementAtoB.ReceiverBusinessIdentity = identityB;
   context.SetLink(onewayAgreementAtoB, "ReceiverBusinessIdentity", identityB);
   identityB.OnewayAgreementReceiver.Add(onewayAgreementAtoB);
   context.AddLink(identityB, "OnewayAgreementReceiver", onewayAgreementAtoB);

   //CREATE THE ONE-WAY AGREEMENT FROM PARTNER B TO PARTNER A
   OnewayAgreement onewayAgreementBtoA = new OnewayAgreement();
   context.AddToOnewayAgreements(onewayAgreementBtoA);

   //LINK THE ONE-WAY AGREEMENT TO THE AGREEMENT ENTITY
   onewayAgreementBtoA.AgreementAsBToA = agreement;
   context.SetLink(onewayAgreementBtoA, "AgreementAsBToA", agreement);
   agreement.OnewayAgreementBToA = onewayAgreementBtoA;
   context.SetLink(agreement, "OnewayAgreementBToA", onewayAgreementBtoA);

   //LINK THE ONE-WAY AGREEMENT TO the BUSINESS IDENTITIES
   onewayAgreementBtoA.SenderBusinessIdentity = identityB;
   context.SetLink(onewayAgreementBtoA, "SenderBusinessIdentity", identityB);
   identityB.OnewayAgreementSender.Add(onewayAgreementBtoA);
   context.AddLink(identityB, "OnewayAgreementSender", onewayAgreementBtoA);
   onewayAgreementBtoA.ReceiverBusinessIdentity = identityA;
   context.SetLink(onewayAgreementBtoA, "ReceiverBusinessIdentity", identityA);
   identityA.OnewayAgreementReceiver.Add(onewayAgreementBtoA);
   context.AddLink(identityA, "OnewayAgreementReceiver", onewayAgreementBtoA);
   ```

13. Finally, you must create the AS2ProtocolSettings entity (for both send and receive-side agreements) and link it to the respective one-way agreement entities. In this step, we’ll finally commit the changes to the context because all the required links are created:

   ```c#
   //CREATE PROTOCOL SETTINGS FOR onewayAgreementAtoB
   AS2ProtocolSettings protSettingsAtoB = new AS2ProtocolSettings();
   protSettingsAtoB.Name = "ProtocolSettingsAtoB" + index;
   protSettingsAtoB.ProtocolName = "AS2";
   context.AddToProtocolSettings(protSettingsAtoB);

   //LINK PROTOCOL SETTING TO onewayAgreementAtoB
   protSettingsAtoB.OnewayAgreement = onewayAgreementAtoB;
   context.SetLink(protSettingsAtoB, "OnewayAgreement", onewayAgreementAtoB);
   onewayAgreementAtoB.ProtocolSettings = protSettingsAtoB;
   context.SetLink(onewayAgreementAtoB, "ProtocolSettings", protSettingsAtoB);

   //CREATE PROTOCOL SETTINGS FOR onewayAgreementBtoA
   AS2ProtocolSettings protSettingsBtoA = new AS2ProtocolSettings();
   protSettingsBtoA.Name = "ProtocolSettingsBtoA" + index;
   protSettingsBtoA.ProtocolName = "AS2";
   context.AddToProtocolSettings(protSettingsBtoA);

   //LINK PROTOCOL SETTING TO onewayAgreementBtoA
   protSettingsBtoA.OnewayAgreement = onewayAgreementBtoA;
   context.SetLink(protSettingsBtoA, "OnewayAgreement", onewayAgreementBtoA);
   onewayAgreementBtoA.ProtocolSettings = protSettingsBtoA;
   context.SetLink(onewayAgreementBtoA, "ProtocolSettings", protSettingsBtoA);

   context.SaveChanges();
   ```

14. Compile and run the program. After the program exits successfully, log on to the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] to verify that the agreement is created. Note that there are still some tasks left before you can use the agreement to process messages. You must now:

   - Upload any certificates required for the AS2 agreement.

   - Specify the route settings to route the message to the destination endpoints, once the message is processed by the agreement.

   - Deploy the agreement. When you run the program, the agreement is created in the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] and its status is set to “Draft”. You must deploy the agreement from the [!INCLUDE[tpm_portal](/Token/tpm_portal_md.md)] before the agreement can start processing messages.

   For more information on these steps, see [Create an AS2 Agreement in Azure BizTalk Services](/Topic/Create_an_AS2_Agreement_in_Azure_BizTalk_Services.md).

## See Also
[Creating .NET Applications Using TPM OM REST API](/Topic/Creating_.NET_Applications_Using_TPM_OM_REST_API.md)

