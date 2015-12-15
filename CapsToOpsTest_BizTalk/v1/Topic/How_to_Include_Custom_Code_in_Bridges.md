---
description: na
keywords: na
pagetitle: How to Include Custom Code in Bridges
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a486c54-dbe7-4c74-9f5a-ffb79b3f950c
---
# How to Include Custom Code in Bridges
Include custom code in your bridge configuration.

While the fixed pattern of bridges (Validate, Enrich, Transform, and Enrich) provided with [!INCLUDE[af_integration](/Token/af_integration_md.md)] serves the requirements of many integration scenarios, sometimes you need to include custom processing as part of your bridge configuration. For example, you might want to convert a message from a flat-file or an XML format to other popular formats, such as XLS or PDF before sending the message out. Similarly, at each stage of message processing, you might want to archive the message to a central data store. In such cases, the fixed pattern of the out-of-box bridges becomes insufficient. To enable such scenarios, bridges include the option of executing custom code at some key stages of the bridge.

This topic provides instructions on how to include custom code using C#.

## How do the bridges include custom code?
The bridge stages that can include custom code have two properties: **On Enter Inspector** and **On Exit Inspector**. For each of these properties, you must enter the assembly-qualified name of the type that includes the custom code you want to execute as part of the bridge.

**Message Inspectors**

To enable including custom code as part of bridge processing, [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides the `IMessageInspector` interface as part of the `Microsoft.BizTalk.Services` namespace. The type that includes the custom code must always implement this interface. For more information, see [API Reference for Azure BizTalk Services](http://msdn.microsoft.com/en-us/library/ed48daa5-5ea6-4ed9-9774-592617953e5d).

## How to include custom code in bridges

1. In the Visual Studio solution that contains the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] project, add a new C# class library project.

2. From the Solution Explorer, add a reference to `Microsoft.BizTalk.Services.dll`. The DLL is available at \Program Files\Microsoft Visual Studio 11.0\Common7\IDE\Extensions\Microsoft\Azure BizTalk Services SDK.

3. Include the `Microsoft.BizTalk.Services` namespace.

   ```
   using Microsoft.BizTalk.Services
   ```

4. Implement the `IMessageInspector` interface. The following example defines a `SetPropertiesInspector` class that we will build to set some custom properties on the message.

   ```
   public class SetPropertiesInspector : IMessageInspector
   {

   }
   ```

5. In the example we use in this topic, let us consider a scenario where as part of the custom component, you need to promote a property on the message that is processed by the bridge. The value that the promoted property must be set to is available only at run time. So at design time, we specify a configurable property that can be associated with a value at run time. To ensure that the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] understands the configurable property, you must adhere to the following considerations.

   - You must define a publicly settable string property.

   - The defined property must have a `PipelinePropertyAttribute` set. If this attribute is not set on the property, the property is not considered for use as part of the custom component configuration.

   - The `PipelinePropertyAttribute` must ideally contain a Name property that must specify the property name with which it will be identified as part of custom code configuration. If no name is specified, the name of the property is considered.

   Here’s an example:

   ```
   [PipelinePropertyAttribute(Name = "PropertyValue")]
   public string Property_Value { get; set; }
   ```
   In this code snippet, we define a string property, **Property_Value**, with a public setter. We set the **PipelinePropertyAttribute** attribute on the property with the name **PropertyValue**.

6. Include your custom logic as part of the class definition. Because the `SetPropertiesInspector` class implements `IMessageInspector`, it must implement the `Execute` task. In this example, we use the `Execute` task to set a custom property on the message.

   > [!IMPORTANT]
   > The class that implements the IMessageInspector interface must include a default constructor that does not take any parameters.

   ```
   public class SetPropertiesInspector : IMessageInspector
   {
       [PipelinePropertyAttribute(Name = "PropertyValue")]
       public string Property_Value { get; set; }       

       public Task Execute(IMessage message, IMessageInspectorContext context)
       {
           return Task.Factory.StartNew(() =>
           {
               if (null != message)
               {
                   string propertyName = "TestProperty";
                   string propertyValue = Property_Value;
                   message.Promote(propertyName, propertyValue);
               }
           });
       }
   }
   ```

7. After creating the class, you must add a reference to it from the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]. This class will be deployed to the cloud as part of the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)] deployment. If the custom class requires any dependent DLLs that must be deployed as well, you must add references to those DLLs as well.

8. For all the DLLs that must be deployed along with the [!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)], set the **CopyLocal** property to **True**.

9. Now that you have defined the custom class, you can include that at any bridge configuration stage that exposes the **On Enter Inspector** and **On Exit Inspector** properties. To include the type, you must provide the assembly-qualified name of the type as part of the property. If you want to include the custom code before the message enters a specific stage, you must include the assembly-qualified name for the **On Enter Inspector** property. Similarly, if you want to include the custom code after the message exits a specific stage, include the assembly-qualified name for the **On Exit Inspector** property. If you have used configuration properties in your custom code, you can also specify the values for those properties here.

   1. Click the ellipsis button **(…)** against the **On Enter Inspector** or **On Exit Inspector** properties for the stage where you want to include the custom code component.

   2. In the dialog box, for the Type text box, specify the fully-qualified assembly name for the custom code component. For example:

      ```
      CustomCodeInspectors.SetPropertiesInspector, SetPropertiesInspector, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null
      ```
      Where, `SetPropertiesInspector` is the type defined under the `CustomCodeInspectors` namespace.

   3. In the Property Configuration box, specify the property name and the value it must be set to. The property name must be the name you specified for the `PipelinePropertyAttribute`. In the code snippet earlier, we set the name to **PropertyValue**. So, in the Property Configuration box, specify the mapping as:

      ```
      PropertyValue = p1
      ```
      Here, **p1** could be a property that was promoted in any of the earlier stages of bridge processing. Note that this sets the value of **TestProperty** to **p1** and not to the value of **p1**.

      ![](/Image/BTS_SVC_CustomCode.gif)

   4. Click **OK**.

## Passing Configurable Values to the Custom Code
On most occasions, the custom code you include as part of the bridge processing might need to work on/with data that is available at runtime, as the bridge is processing the message. For example, there could be a scenario where you need to promote a property on the message but the value for that promoted property is dynamically available only at runtime, and cannot be set while you are writing the custom component. This calls for a way of using configurable properties as part of the custom code component. [!INCLUDE[af_integration](/Token/af_integration_md.md)] provides a **PipelinePropertyAttribute** property attribute, that can specified for a publicly settable string property within the class that implements the `IPipelineMessageInspector` interface. The property that has the attribute specified can be set in the inspectors in the bridge configuration surface at design time.

## Which stages in the bridge can include custom code?
In an **[!INCLUDE[one-way](/Token/one-way_md.md)]**, the following stages can include custom code:

- Decode

- Validate

- Enrich

- Transform

- Enrich (post-Transform)

- Encode

In an **[!INCLUDE[request_response](/Token/request_response_md.md)]**, the following stages can include custom code:

- Request side

   - Validate

   - Enrich

   - Transform

   - Enrich (post-Transform)

- Response side

   - Enrich

   - Transform

   - Enrich (post-Transform)

In a **[!INCLUDE[passthru](/Token/passthru_md.md)]**, Enrich is the only stage that can include custom code.

## See Also
[Add Source, Destination, and Bridge Messaging Endpoints](/Topic/Add_Source,_Destination,_and_Bridge_Messaging_Endpoints.md)

