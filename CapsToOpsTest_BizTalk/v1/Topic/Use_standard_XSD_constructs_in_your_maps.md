---
description: na
keywords: na
pagetitle: Use standard XSD constructs in your maps
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a028e9a-b0e7-4d44-a121-38b876f8020f
---
# Use standard XSD constructs in your maps
[!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)] support now includes the following:

- All standard schema constructs used in complex schemes, including xs:extension and xs:restriction types, are fully supported in design time and runtime. These derived types are typically used in Salesforce, OAGIS, and GJXDM schemas.

- All the allowed nodes under the ComplexType are fully supported in design time and run time.

- Implicit conditional mapping for Derived Types in the source schema is fully supported.

> [!IMPORTANT]
> &lt;xs:list&gt; constructs contain a list of string values. All the values in the construct are treated as one single element. For example, there is an element that is a string list type. The element contains a list of names: “Name_1 Name_2 Name_3”. Since this is a list, these names are read as [“Name_1”, “Name_2”, “Name_3”]. However, this is not supported for the current release. In the current release, the list is considered to be one single element.

## Derived Types: xs:extension and xs:restriction
'When you create a new complex type in XML schema, you can enter xs:extension or xs:restriction and specify the base complex type to create derived types.

## Implicit conditional mapping
Using derived XML Data Types, you can do ‘OR’ conditional mapping. Looking at the following [!INCLUDE[transform](/Token/transform_md.md)], the nodes under CustomerAddress in the Source schema are mapped to CustomerAddress in the Target schema. The String Concatenate operation concatenates the appropriate strings based on the type – “USAddress” or “UKAddress”:

![](/Image/BtsSvc_USUKAddress.jpg)

When you create a complex type within a schema, you specify the “type”. For example, you enter **type=“Address”**:

![](/Image/BtsSvc_AddressType.jpg)

“Address” and its elements (“street” and “city”) are now the base:

![](/Image/BtsSvc_AddressBase.jpg)

You can create new elements that are based off “Address” (and its elements – “street” and “city”). For example, you can create “USAddress” based off “Address” to add elements, like “state” and “zip”:

![](/Image/BtsSvc_USAddress.jpg)

“USAddress” is a defined as derived type by entering **&lt;xs:extension base="Address"&gt;** in the schema. When the schema executes and the incoming message uses “USAddress”, then the “state” and “zip” values are added to the existing “street” and “city” values. All four values are in the output message as CustomerAddress. 
OR
When the schema executes and the incoming message uses “UKAddress”, then the “postcode” and “exportcode” values are added to the existing “street” and “city” values. All four values are in the output message as CustomerAddress. 
OR
When the schema executes and the incoming message is “Address” or doesn’t specify a derived type (“USAddress” or “UKAddress”), then only the base “Address” values (“street” and “city”) are in the output message as CustomerAddress.

## Errors and Warnings

- **Derived Types at the Same Level**

   When a schema has two equivalent derived types (which can be at the same level or a different level), you cannot create links from elements within these two separate derived types. For example, the following schema has an “Email” derived type and a “MassEmail” derived type at the same level:

   ![](/Image/BtsSvc_Links2DTypes.jpg)

   When you create the links, the following error occurs:

**String Concatenate Operation labeled 'AddFirstNameLastName' has input links from elements or attributes under more than one derived type element (xs:extension or xs:restriction) at same level in Source schema.**

- **Derived Types at Different Levels**

   When a [!INCLUDE[mapop](/Token/mapop_md.md)] has a link from two non-equivalent derived types (which may or may be at the same level), it returns a warning. For example, the following [!INCLUDE[transform](/Token/transform_md.md)] has a link from the “toAddress” derived type under “MassEmail” and a link from the “Location” and “City” derived types under “ContactAddress”:

   ![](/Image/BtsSvc_LinksOnlyDTypes.jpg)

   When you create the links, the following warning occurs:

**String Concatenate operation labeled 'AddToAddressAndLocation' has input links from elements or attributes under more than one derived type element(xs:extension or xs:restriction) in Source schema. This can result in an output XML instance that violates Destination schema.**

- **Links from a Derived Type and a Normal Type**

   When a [!INCLUDE[mapop](/Token/mapop_md.md)] has a link from a derived type and a normal type, it returns a warning. For example, the following [!INCLUDE[transform](/Token/transform_md.md)] has a link from the “FirstName” derived type under “Email” and a link from the “Record” normal type:

   ![](/Image/BtsSvc_LinksDTypes2NTypes.jpg)

   When you create the links, the following warning occurs:

**String Concatenate operation labeled 'AddFirstNameLastName' has input links from elements or attributes under a derived type element (xs:extension or xs:restriction) and a normal type element in Source schema. This can result in an output XML instance that violates Destination schema.**

## Next
[Use Derived Types in Mapping Scenarios and Examples](/Topic/Use_Derived_Types_in_Mapping_Scenarios_and_Examples.md)

## More Transforms topics
[Convert a BizTalk map to a BizTalk Services Transform](/Topic/Convert_a_BizTalk_map_to_a_BizTalk_Services_Transform.md)

[Transforms&#47;Maps Best Practices](/Topic/Transforms/Maps_Best_Practices.md)

[Loop and Scope Examples in map or transforms](/Topic/Loop_and_Scope_Examples_in_map_or_transforms.md)

**[Azure BizTalk Services Resources on the TechNet Wiki](http://social.technet.microsoft.com/wiki/contents/articles/11426.azure-biztalk-services-resources-on-the-technet-wiki.aspx)**

