---
description: na
keywords: na
pagetitle: Step 1: Build and Deploy the Relay Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a7ee8f7-d76d-41b2-abe8-4c8822130f41
---
# Step 1: Build and Deploy the Relay Services
This step of the tutorial demonstrates how to create a relay service that receives a message from the [!INCLUDE[bridge](/Token/bridge_md.md)] and generates a response for the insurance quotes that come in. The service also stamps the response with the message headers before sending it back to the [!INCLUDE[bridge](/Token/bridge_md.md)]. As per the business scenario, this step demonstrates how to create two services. One service receives insurance quotes less than $10000 and the other receives insurance quotes more than $10000. This scenario could also have used an external WCF service instead, but using relay services provides the option of extensibility. Relay services can serve as an interface endpoint to more elaborate systems behind an organization’s firewall. For example, even though Northwind Traders receive and validate the insurance quotes over the cloud, it might still be storing the message data in a line-of-business (LOB) application behind a firewall. Or, after receiving the message it might be triggering off a workflow in SharePoint Server. So, using a relay service provides the capability to create hybrid applications. For more information, see [How to Use the Service Bus Relay Service](http://go.microsoft.com/fwlink/?LinkId=252250) (http://go.microsoft.com/fwlink/?LinkId=252250).

This topic does not create a service from scratch. It only presents the code that receives the message and generates a response. You can download the entire code from [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=252395).

### To build and deploy RelayReceiverServiceA

1. Download the [MSDN Code Gallery sample](http://go.microsoft.com/fwlink/?LinkId=252395). Extract the package contents and open the **RelayReceiverServiceA** project.

2. From Solution Explorer, double-click and open **RouteTwoWayReceiveService.cs** and verify the following code block:

   1. Verify the following namespaces are present:

      ```
      using System.Collections.Generic;
      using System.Linq;
      using System.Runtime.Serialization;
      using System.Text;
      using System.ServiceModel.Dispatcher;
      using System.Xml;
      ```

   2. Verify the existing code block is present. This code block receives a message from the bridge, stamps the required headers, and sends the response back to the bridge.

      ```
      public Message ReceiveAndReply(Message received)
      {
          //Create a message buffer. All the operations on the message, reading or writing, will be done
          //on copies created from this buffer
          MessageBuffer buffer = received.CreateBufferedCopy(Int32.MaxValue);

          try
          {
              //Create a tempfile variable to store the filename to which the message will be written. 
              //This ensures that every time a file with a unique name is created and the previous message
              //is not overwritten.
              var tempFile = Path.Combine(Directory.GetCurrentDirectory(), "Received_Message" + DateTime.Now.Ticks + ".xml");
              XmlWriterSettings xmlsetting = new XmlWriterSettings();
              xmlsetting.ConformanceLevel = ConformanceLevel.Auto;

              //Create an XML writer to write the message to a file
              using (XmlWriter xmlWriter = XmlWriter.Create(tempFile, xmlsetting))
              {
                  try
                  {
                      //Create a copy of the message from the buffer. Perform all the operations on that copy.
                      Message copy1 = buffer.CreateMessage();
                      copy1.WriteMessage(xmlWriter);
                      Console.WriteLine();
                        Console.WriteLine("*************************************************************************");
                        Console.WriteLine("Message processed successfully. Request message saved at : " + tempFile);
                        Console.WriteLine("*************************************************************************");

                  }
                  catch (Exception e)
                  {
                      Console.WriteLine("Exception : {0}", e);
                  }

                  //Close the XML writer
                  xmlWriter.Close();
              }
          }
          catch
          {
              Console.WriteLine("An error occurred during processing. Please try again.");
          }

          //Create another copy of the original message. This copy will be used to generate the response        
          Message copy2 = buffer.CreateMessage();

          //Read the message body
          XmlDictionaryReader messageBody = null;
          messageBody = copy2.GetReaderAtBodyContents();

          //Create the response message
          Message newMsg = null == messageBody ? Message.CreateMessage(copy2.Version, "*") : Message.CreateMessage(copy2.Version, "*", messageBody);

          //Create two new headers, MsgStatus and Eligibility, and assign values to them per
          //the business scenario
          MessageHeader status = MessageHeader.CreateHeader("MsgStatus", "http://Northwind.com/insurance/ACORD1/xml/", "Success");
          MessageHeader eligibility = MessageHeader.CreateHeader("Eligibility", "http://Northwind.com/insurance/ACORD1/xml/", "ApprovedForSmallAmounts");

          //Add the new headers to the newly constructed message
          newMsg.Headers.Add(status);
          newMsg.Headers.Add(eligibility);
          return newMsg;
      }
      ```
      Notice the values assigned to the headers **MsgStatus** and **Eligibility**. These values were defined as part of the [Business Scenario](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md#BKMK_Scenario).

   3. The **RouteTwoWayReceiveService** class implements the **IRouteTwoWayReceiveService** interface. So, make sure the interface definition (**IRouteTwoWayReceiveService.cs**) includes the **ReceiveAndReply** method declaration.

      ```
      Message ReceiveAndReply(Message received)
      ```

   4. Press **F6** to build the solution.

   5. Open a command prompt and navigate to location for the \bin\Debug folder for the project. Type the following command:

      ```
      RelayReceieverServiceA.exe 2 <ServiceBusNamespace> owner <Issuerkey> /RelayReceiverServiceA
      ```
      Here, ‘2’ denotes that you are deploying a two-way relay service. The relative address **/RelayReceiverServiceA** must be the same that you specified in the procedure [To represent RelayReceiverServiceA in the project](/Topic/Step_5__Connect_Bridge_and_Services.md#BKMK_RelayServiceA).

      After the relay service is successfully deployed, the command prompt displays the following:

      ```
      Starting the RelayReceiverService...
      2 Way RelayReceiverService started at address: https://<your_servicebus_namespace>.servicebus.windows.net/RelayReceiverServiceA/
      Hit ENTER to stop the service.
      ```

### To build and deploy RelayReceiverServiceB

1. From the sample you downloaded from the [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=252395) open the **RelayReceiverServiceB** project.

2. From Solution Explorer, double-click and open **RouteTwoWayReceiveService.cs** and verify the following code block:

   1. Verify the following namespaces are present:

      ```
      using System.Collections.Generic;
      using System.Linq;
      using System.Runtime.Serialization;
      using System.Text;
      using System.ServiceModel.Dispatcher;
      using System.Xml;
      ```

   2. Replace the existing code block with the following code block:

      ```
      public Message ReceiveAndReply(Message received)
      {
          //Create a message buffer. All the operations on the message, reading or writing, will be done
          //on copies created from this buffer
          MessageBuffer buffer = received.CreateBufferedCopy(Int32.MaxValue);

          try
          {
              //Create a tempfile variable to store the filename to which the message will be written. 
              //This ensures that every time a file with a unique name is created and the previous message
              //is not overwritten.
              var tempFile = Path.Combine(Directory.GetCurrentDirectory(), "Received_Message" + DateTime.Now.Ticks + ".xml");
              XmlWriterSettings xmlsetting = new XmlWriterSettings();
              xmlsetting.ConformanceLevel = ConformanceLevel.Auto;

              //Create an XML writer to write the message to a file
              using (XmlWriter xmlWriter = XmlWriter.Create(tempFile, xmlsetting))
              {
                  try
                  {
                      //Create a copy of the message from the buffer. Perform all the operations on that copy.
                      Message copy1 = buffer.CreateMessage();
                      copy1.WriteMessage(xmlWriter);
                      Console.WriteLine();
                        Console.WriteLine("*************************************************************************");
                        Console.WriteLine("Message processed successfully. Request message saved at : " + tempFile);
                        Console.WriteLine("*************************************************************************");
                  }
                  catch (Exception e)
                  {
                      Console.WriteLine("Exception : {0}", e);
                  }

                  //Close the XML writer
                  xmlWriter.Close();
              }
          }
          catch
          {
              Console.WriteLine("An error occurred during processing. Please try again.");
          }

          //Create another copy of the original message. This copy will be used to generate the response        
          Message copy2 = buffer.CreateMessage();

          //Read the message body
          XmlDictionaryReader messageBody = null;
          messageBody = copy2.GetReaderAtBodyContents();

          //Create the response message
          Message newMsg = null == messageBody ? Message.CreateMessage(copy2.Version, "*") : Message.CreateMessage(copy2.Version, "*", messageBody);

          //Create two new headers, MsgStatus and Eligibility, and assign values to them per
          //the business scenario
          MessageHeader status = MessageHeader.CreateHeader("MsgStatus", "http://Northwind.com/insurance/ACORD1/xml/", "Success");
          MessageHeader eligibility = MessageHeader.CreateHeader("Eligibility", "http://Northwind.com/insurance/ACORD1/xml/", "ApprovedForLargeAmounts");

          //Add the new headers to the newly constructed message
          newMsg.Headers.Add(status);
          newMsg.Headers.Add(eligibility);
          return newMsg;
      }
      ```
      Notice the values assigned to the headers **MsgStatus** and **Eligibility**. These values were defined as part of the [Business Scenario](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md#BKMK_Scenario).

   3. The **RouteTwoWayReceiveService** class implements the **IRouteTwoWayReceiveService** interface. So, make sure the interface definition (**IRouteTwoWayReceiveService.cs**) includes the **ReceiveAndReply** method declaration.

      ```
      Message ReceiveAndReply(Message received)
      ```

   4. Press **F6** to build the solution.

   5. Open a command prompt and navigate to location for the \bin\Debug folder for the project. Type the following command:

      ```
      RelayReceieverServiceB.exe 2 <ServiceBusNamespace> owner <Issuerkey> /RelayReceiverServiceB
      ```
      Here, ‘2’ denotes that you are deploying a two-way relay service. The relative address **/RelayReceiverServiceB** must be the same that you specified in the procedure [To represent RelayReceiverServiceB in the project](/Topic/Step_5__Connect_Bridge_and_Services.md#BKMK_RelayServiceB).

      After the relay service is successfully deployed, the command prompt displays the following:

      ```
      Starting the RelayReceiverService...
      2 Way RelayReceiverService started at address: https://<your_servicebus_namespace>.servicebus.windows.net/RelayReceiverServiceB/
      Hit ENTER to stop the service.
      ```

## See Also
[Tutorial: Using BizTalk Service Bridges to Send and Receive Messages from Service Bus Relay Service](/Topic/Tutorial__Using_BizTalk_Service_Bridges_to_Send_and_Receive_Messages_from_Service_Bus_Relay_Service.md)

