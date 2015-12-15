---
description: na
keywords: na
pagetitle: Include custom code to insert purchase order into SQL Server
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca9c0d7b-2063-4034-8856-10935e4f6a6e
---
# Include custom code to insert purchase order into SQL Server
This topic provides instructions on how to include a custom code component as part of bridge configuration. In this project, we use the custom code component to send a message to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] that we configured in the previous step. When a message with a valid schema is sent to that [!INCLUDE[lobrelay](/Token/lobrelay_md.md)], the data from the message is written to a SQL Server database. But why do we use custom code to insert data into a SQL Server database when we could use [!INCLUDE[lobconnect](/Token/lobconnect_md.md)] instead? That is because the [!INCLUDE[af_integration](/Token/af_integration_md.md)] bridge can route messages to a single destination only using the bridge designer. For this scenario, we need to send the message to two destinations, the blob and [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] endpoint. So, we use custom code to send the message to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] endpoint and the out-of-the-box bridge designer to send the message to the [!INCLUDE[azure_2](/Token/azure_2_md.md)] blob.

### To create a custom code component

1. In the Visual Studio solution that contains the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] project, add a new C# class library project. For this tutorial, name the project: **CustomCode_PurchaseOrder**.

2. Add the following references:

   - Microsoft.BizTalk.Services. The DLL is available in \Program Files\Microsoft Visual Studio 11.0\Common7\IDE\Extensions\Microsoft\[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] SDK.

   - Microsoft.ServiceBus

   - System.Runtime.Serialization

   - System.ServiceModel

   - System.ServiceModel.Channels

3. Add the following namespaces to the existing list:

   - System.IO

   - System.Xml

   - System.ServiceModel

   - Microsoft.BizTalk.Services

   - Microsoft.ServiceBus

4. Implement the `IMessageInspector` interface. The following example defines a `WritePOToSQL` class that we will build to send an XML message to the [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] endpoint.

   ```
   namespace CustomCode_PurchaseOrder
   {
     public class WritePOToSQL : IMessageInspector
     {

     }
   }
   ```

5. Include your custom logic as part of the class definition. Because the `WritePOToSQL` class implements `IMessageInspector`, it must implement the `Execute` task. In this tutorial, we use the `Execute` task to create an XML message (with the same schema required to insert the data into the SQL Server database) from the message received from the customer. The XML message is then sent to the SQL Server [!INCLUDE[lobrelay](/Token/lobrelay_md.md)] so that it is inserted into the **Orders** table in the **CloudCarDatabase**.

   > [!IMPORTANT]
   > The class that implements the `IMessageInspector` interface must include a default constructor that does not take any parameters.

   ```
   public class WritePOToSQL : IMessageInspector
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

                   XmlNode infoNode = xm.GetElementsByTagName("CustomerInfo")[0];
                   string customerName = infoNode.Attributes["Name"].Value;
                   string customerEmail = infoNode.Attributes["Email"].Value;
                   string customerPhone = infoNode.Attributes["Phone"].Value;
                   string supplierName = xm.GetElementsByTagName("SupplierName")[0].InnerText;
                   string orderId = xm.GetElementsByTagName("OrderId")[0].InnerText;

                   // CREATE A NEW XML DOCUMENT WITH THE SCHEMA REQUIRED TO INSERT 
                   // THE PURCHASE ORDER MESSAGE INTO A SQL SERVER DATABASE
                   XmlDocument xml = new XmlDocument();
                   XmlElement root = xml.CreateElement("ns0:Insert", @"http://schemas.microsoft.com/Sql/2008/05/TableOp/dbo/Orders");
                   xml.AppendChild(root);
                   root.SetAttribute("xmlns:ns0", @"http://schemas.microsoft.com/Sql/2008/05/TableOp/dbo/Orders");
                   XmlElement rows = xml.CreateElement("ns0:Rows", @"http://schemas.microsoft.com/Sql/2008/05/TableOp/dbo/Orders");
                   root.AppendChild(rows);
                   XmlElement orders = xml.CreateElement("ns1:Orders", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                   rows.AppendChild(orders);

                   orders.SetAttribute("xmlns:ns1", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                   XmlElement child1 = xml.CreateElement("ns1:CustomerName", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                   child1.InnerText = customerName;
                   XmlElement child2 = xml.CreateElement("ns1:CustomerEmail", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                   child2.InnerText = customerEmail;
                   XmlElement child3 = xml.CreateElement("ns1:CustomerPhone", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                   child3.InnerText = customerPhone;
                   XmlElement child4 = xml.CreateElement("ns1:SupplierName", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                   child4.InnerText = supplierName;
                   XmlElement child5 = xml.CreateElement("ns1:OrderId", @"http://schemas.microsoft.com/Sql/2008/05/Types/Tables/dbo");
                   child5.InnerText = orderId;
                   orders.AppendChild(child1);
                   orders.AppendChild(child2);
                   orders.AppendChild(child3);
                   orders.AppendChild(child4);
                   orders.AppendChild(child5);

                   StringWriter sw = new StringWriter();
                   XmlTextWriter tx = new XmlTextWriter(sw);
                   xml.WriteTo(tx);

                   string str = sw.ToString();
                   MemoryStream stream = new MemoryStream();
                   StreamWriter streamWriter = new StreamWriter(stream);
                   streamWriter.Write(str);
                   streamWriter.Flush();
                   stream.Seek(0, SeekOrigin.Begin);

                   // SEND THE XML MESSAGE TO THE RELAY ENDPOINT 
                   // DEPLOYED ON SERVICE BUS
                   BasicHttpRelayBinding binding = new BasicHttpRelayBinding();
                   EndpointAddress address = new EndpointAddress("https://<servicebus_ns>.servicebus.windows.net/SQLtarget/orders/");
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
                       System.ServiceModel.Channels.Message request = System.ServiceModel.Channels.Message.CreateMessage(System.ServiceModel.Channels.MessageVersion.Soap11, @"TableOp/Insert/dbo/Orders", xdr);
                       System.ServiceModel.Channels.Message reply = channel.Request(request);
                       context.Tracer.TraceEvent(TraceEventType.Information, reply.ToString());
                       reply.Close();
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
               });
           }
   }
   ```
   Add a strong name key to the project to sign the assembly and then build the project. This will create the **CustomCode_PurchaseOrder.dll**.

6. After building the project, you must add a reference to it from the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] so that the class is deployed to the cloud as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] deployment. If the custom class has a dependency on any other DLLs they must be deployed as well, and you must add references to those DLLs too.

   Within the **CloudCar_Integration_PurchaseOrder** project, right-click **References**, and then select **Add Reference**. Browse to the location for **CustomCode_PurchaseOrder.dll**, and select the DLL to add a reference to the DLL. After you have added the reference, ensure the **Copy Local** property for the DLL is set to **True**.

7. For this tutorial, we are sending the message to the CloudCarDatabase *before* the message is transformed. To do so, double-click the [!INCLUDE[one-way](/Token/one-way_md.md)], select the **Transform** stage, and select the ellipsis (…) against the **On Enter Inspector** property. In the **Type** text box, enter the fully qualified assembly name for the custom code. For example, the fully qualified assembly name for the CustomCode_PurchaseOrder.dll could be similar to:

   ```
   CustomCode_PurchaseOrder.WritePOToSQL, CustomCode_PurchaseOrder, Version=1.0.0.0, Culture=neutral, PublicKeyToken=<token>
   ```

8. Save the changes then build the project.

## See Also
[Create a BizTalk Service project to process purchase orders](/Topic/Create_a_BizTalk_Service_project_to_process_purchase_orders.md)

