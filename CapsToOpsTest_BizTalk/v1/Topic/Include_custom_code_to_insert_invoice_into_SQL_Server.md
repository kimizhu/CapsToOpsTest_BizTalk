---
description: na
keywords: na
pagetitle: Include custom code to insert invoice into SQL Server
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edcfee5d-2174-4c80-a6a9-a2d1e9bef977
---
# Include custom code to insert invoice into SQL Server
This topic provides instructions on how to include a custom code component as part of bridge configuration. For this project, we use the custom code component to send a message to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] that we configured in the previous step, and to send an e-mail to the customer with the status of the order they placed.

### To create a custom code component

1. In the Visual Studio solution that contains the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] project, add a new C# class library project. For this tutorial, name the project as **CustomCode_Invoice**.

2. Add the following references:

   - Microsoft.BizTalk.Services. The DLL is available at \Program Files\Microsoft Visual Studio 11.0\Common7\IDE\Extensions\Microsoft\[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK.

   - Microsoft.ServiceBus

   - System.Runtime.Serialization

   - System.ServiceModel

   - System.ServiceModel.Channels

   This custom code component must also send e-mails to the customer. To do so, we use the SendGrid service from the custom code component. SendGrid Nuget package is the easiest way to reference the SendGrid API from your application code. For instructions on how to add reference to SendGrid .NET APIs, see [http://go.microsoft.com/fwlink/p/?LinkId=389151](http://go.microsoft.com/fwlink/p/?LinkId=389151).

3. Include the following namespaces, in addition to the existing ones:

   - System.IO

   - System.Xml

   - System.ServiceModel

   - Microsoft.BizTalk.Services

   - Microsoft.ServiceBus

   - System.Net

   - System.Net.Mail

   - SendGridMail

   - SendGridMail.Transport

4. Implement the `IMessageInspector` interface. The following example defines a `WriteInvoiceToSQL` class that we will build to send an XML message to [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] endpoint.

   ```
   namespace CustomCode_Invoice
   {
     public class WriteInvoiceToSQL : IMessageInspector
     {

     }
   }
   ```

5. Include your custom logic as part of the class definition. Because the `WriteInvoiceToSQL` class implements `IMessageInspector`, it must implement the `Execute` task. In this tutorial, we use the `Execute` task to create an XML message (with the same schema required to insert the data into SQL Server database) from the message received from the customer. The XML message is then sent to the SQL Server [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] so that it is inserted into the **Invoice** table in the **CloudCarDatabase**.

   > [!IMPORTANT]
   > The class that implements the `IMessageInspector` interface must include a default constructor that does not take any parameters.

   ```
   public class WriteInvoiceToSQL : IMessageInspector
       {
           public Task Execute(IMessage input, IMessageInspectorContext context)
           {
               return Task.Factory.StartNew(() =>
               {
                   // CONFIGURE TRACING
                   context.Tracer.TraceEvent(TraceEventType.Information, "**** ENTERED **** ");
                   Stream ms = input.Data;
                   ms.Position = 0;
                   int l = (int)ms.Length;
                   byte[] bytes = new byte[l];
                   ms.Read(bytes, 0, l);
                   string body = Encoding.UTF8.GetString(bytes);
                   StringBuilder newString = new StringBuilder();
                   char ch;

                   for (int i = 0; i < body.Length; i++)
                   {
                       ch = body[i];
                       if ((ch < 0x00FD && ch > 0x001F) || ch == '\t' || ch == '\n' || ch == '\r')
                       {
                           newString.Append(ch);
                       }
                   }
                   context.Tracer.TraceEvent(TraceEventType.Information, " **** MESSAGE BODY : {0} **** ", newString);

                   // LOAD THE XML DOCUMENT AND EXTRACT REQUIRED ELEMENTS OR ATTRIBUTES
                   XmlDocument xm = new XmlDocument();
                   xm.LoadXml(newString.ToString());

                   XmlNodeList nodeList = xm.DocumentElement.ChildNodes;
                   string OrderId = xm.GetElementsByTagName("OrderId")[0].InnerText;
                     string Item = xm.GetElementsByTagName("Item")[0].InnerText;
                     string Quantity = xm.GetElementsByTagName("Quantity")[0].InnerText;
                     string OrderStatus = xm.GetElementsByTagName("OrderStatus")[0].InnerText;
                     string Email = xm.GetElementsByTagName("Email")[0].InnerText;

                   // CREATE A NEW XML DOCUMENT WITH THE SCHEMA REQUIRED TO INSERT 
                     // THE INVOICE MESSAGE INTO A SQL SERVER DATABASE
                   if (OrderStatus.Equals("accepted", StringComparison.CurrentCultureIgnoreCase))
                   {
                       XmlDocument xml = new XmlDocument();
                       XmlElement root = xml.CreateElement("Insert", @"http://schemas.microsoft.com/Sql/2008/05/TableOp/dbo/Invoice");
                       xml.AppendChild(root);
                       root.SetAttribute("xmlns", @"http://schemas.microsoft.com/Sql/2008/05/TableOp/dbo/Invoice");
                       XmlElement rows = xml.CreateElement("Rows", @"http://schemas.microsoft.com/Sql/2008/05/TableOp/dbo/Invoice");
                       root.AppendChild(rows);
                       XmlElement invoice = xml.CreateElement("Invoice", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                       rows.AppendChild(invoice);
                       invoice.SetAttribute("xmlns", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                       XmlElement child1 = xml.CreateElement("OrderId", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                          child1.InnerText = OrderId;
                          XmlElement child2 = xml.CreateElement("Item", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                          child2.InnerText = Item;
                          XmlElement child3 = xml.CreateElement("Quantity", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                          child3.InnerText = Quantity;
                          XmlElement child4 = xml.CreateElement("OrderStatus", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                          child4.InnerText = OrderStatus;
                          XmlElement child5 = xml.CreateElement("Email", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                          child5.InnerText = Email;
                          invoice.AppendChild(child1);
                          invoice.AppendChild(child2);
                          invoice.AppendChild(child3);
                          invoice.AppendChild(child4);
                          invoice.AppendChild(child5);

                       StringWriter sw = new StringWriter();
                       XmlTextWriter tx = new XmlTextWriter(sw);
                       xml.WriteTo(tx);

                       string str = sw.ToString();
                       context.Tracer.TraceEvent(TraceEventType.Information, " **** END XML **** : {0} ", str);

                       MemoryStream stream = new MemoryStream();
                       StreamWriter streamWriter = new StreamWriter(stream);
                       streamWriter.Write(str);
                       streamWriter.Flush();
                       stream.Seek(0, SeekOrigin.Begin);

                       // SEND THE XML MESSAGE TO THE RELAY ENDPOINT 
                          // DEPLOYED ON SERVICE BUS
                       BasicHttpRelayBinding binding = new BasicHttpRelayBinding();
                       EndpointAddress address = new EndpointAddress("https://<servicebus_ns>.servicebus.windows.net/sqltarget/invoice/");
                       ChannelFactory<System.ServiceModel.Channels.IRequestChannel> factory = new ChannelFactory<System.ServiceModel.Channels.IRequestChannel>(binding, address);

                       TransportClientEndpointBehavior sharedSecretServiceBusCredential = new TransportClientEndpointBehavior();
                       TokenProvider tokenProvider = TokenProvider.CreateSharedSecretTokenProvider("owner", "<issuer_key>");
                       sharedSecretServiceBusCredential.TokenProvider = tokenProvider;
                       factory.Endpoint.Behaviors.Add(sharedSecretServiceBusCredential);

                       System.ServiceModel.Channels.IRequestChannel channel = factory.CreateChannel();

                       try
                       {
                           channel.Open();
                           XmlDictionaryReader xdr = XmlDictionaryReader.CreateTextReader(stream, new XmlDictionaryReaderQuotas());
                           System.ServiceModel.Channels.Message request = System.ServiceModel.Channels.Message.CreateMessage(System.ServiceModel.Channels.MessageVersion.Soap11, @"TableOp/Insert/dbo/Invoice", xdr);
                           System.ServiceModel.Channels.Message reply = channel.Request(request);
                           context.Tracer.TraceEvent(TraceEventType.Information, reply.ToString());
                           reply.Close();

                           /// SEND EMAIL USING SENDGRID
                           var myMessage = SendGrid.GetInstance();

                           // Add the message properties.
                           myMessage.From = new MailAddress("<enter from address here>");

                           // Add multiple addresses to the To field.
                           List<String> recipients = new List<String>
                           {
                               Email                            
                           };

                           myMessage.AddTo(recipients);

                           myMessage.Subject = "Your order details";

                           //Add the HTML and Text bodies
                           myMessage.Html = "<p>Your order number is: " + OrderId + "</p>" +
                               "<p>You ordered for: " + Item + "</p>" +
                               "<p>Quantity ordered is: " + Quantity + "</p>" +
                               "<p>Your order has been: " + OrderStatus + "</p>" +
                               "<p>Thank You!</p>";

                           var username = "<sendgrid_account_username>";
                           var pswd = "<sendgrid_account_password>";
                           var credentials = new NetworkCredential(username, pswd);

                           var transportSMTP = SMTP.GetInstance(credentials);
                           transportSMTP.Deliver(myMessage);
                       }
                       catch (Exception ex)
                       {
                           context.Tracer.TraceEvent(TraceEventType.Information, ex.Message);
                       }
                       finally
                       {
                           channel.Close();
                           factory.Close();
                       }
                   }
               });
           }
       }
   ```
   Add a strong name key to the project to sign the assembly and then build the project. This will create the **CustomCode_Invoice.dll**.

   > [!IMPORTANT]
   > While building the custom code project, you might get an error suggesting that the SendGrid assembly is not signed with a strong name. In such a case, you must first sign the SendGrid assembly and then rebuild the project. To do so, use ildasm to first disassemble the SendGrid assembly into a .il file and .res file
   > 
   > `ildasm myTest.dll /out:myTest.il`
   > 
   > Then reassemble it by using your key
   > 
   > `ilasm myTest.il /res:myTest.res /dll /key:myTest.snk /out:myTest.dll`

6. After building the project, you must add a reference to it from the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. This class will be deployed to the cloud as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] deployment. If the custom class requires any dependent DLLs that must be deployed as well, you must add references to those DLLs as well.

   Within the **CloudCar_Integration_Invoice** project, right-click **References**, and then select **Add Reference**. Browse to the location for **CustomCode_Invoice.dll**, and select the DLL to add a reference to the DLL. After you have added the reference, make sure the **Copy Local** property for the DLL is set to **True**. Repeat this step for **SendGrid.dll** as well.

7. For this tutorial, we want to send the message to the CloudCarDatabase after the message is transformed to the invoice format expected by Contoso, Ltd. To do so, double-click the [!INCLUDE[one-way](/Token/one-way_md.md)], select the **Transform** stage, and select the ellipsis (…) against the **On Exit Inspector** property. In the **Type** text box, enter the fully qualified assembly name for the custom code. For example, the fully qualified assembly name for the CustomCode_Invoice.dll could be similar to:

   ```
   CustomCode_Invoice.WriteInvoiceToSQL, CustomCode_Invoice, Version=1.0.0.0, Culture=neutral, PublicKeyToken=<token>
   ```

8. Save changes to the project, and then build the project.

## See Also
[Create a BizTalk Service project to process invoices](/Topic/Create_a_BizTalk_Service_project_to_process_invoices.md)

