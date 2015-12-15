---
description: na
keywords: na
pagetitle: Use Derived Types in Mapping Scenarios and Examples
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8db0ba6-2cdd-4546-a561-afe1b96e5865
robots: noindex,nofollow
---
# Use Derived Types in Mapping Scenarios and Examples
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Usage scenarios and examples when using Derived Types. Specifically:</para>
    <para>
      <link xlink:href="a8db0ba6-2cdd-4546-a561-afe1b96e5865#BKMK_Terms">Definitions You Need to Know</link>
    </para>
    <para>
      <link xlink:href="a8db0ba6-2cdd-4546-a561-afe1b96e5865#BKMK_DToN">Scenario: Links from Derived Type to Normal Type</link>
    </para>
    <para>
      <link xlink:href="a8db0ba6-2cdd-4546-a561-afe1b96e5865#BKMK_NToD">Scenario: Links from Normal Type to Derived Type</link>
    </para>
    <para>
      <link xlink:href="a8db0ba6-2cdd-4546-a561-afe1b96e5865#BKMK_DToD">Scenario: Links from Derived Type to Derived Type</link>
    </para>
  </introduction>
  <section address="BKMK_Terms">
    <title>Definitions You Need to Know</title>
    <content>
      <para>
        <legacyBold>Normal Type element or node</legacyBold>: Any complex type element in the schema that does not have any other complex types deriving from it.</para>
      <para>
        <legacyBold>Derived Type element or node</legacyBold>: Any complex type element in the schema that is derived from a base complex element with “xs:extension” or “xs:restriction”.</para>
      <para>
        <legacyBold>Multi Type element or node</legacyBold>: Any complex type element in the schema that has one (or more) complex types deriving from it.</para>
    </content>
  </section>
  <section address="BKMK_DToN">
    <title>Scenario: Links from Derived Type to Normal Type</title>
    <content>
      <para>In a <token>transform</token>, the Source schema has a Derived Type and the Target schema has a Normal Type. Links from a Derived Type are only evaluated when the “xsi:type” value in the input XML message matches the Derived Type. If no Derived Type is specified, it is treated as the base type. </para>
      <para>In the following example, the Source schema has “Email” as the base. “MassEmailMessage” is a Derived Type of “Email”, and “SingleEmailMessage” is a Derived Type of “Email”. The Target schema has all Normal Types:</para>
      <mediaLink>
        <image xlink:href="ea19efc5-0a77-4a57-948c-5227019e5c05" />
      </mediaLink>
      <para>
        <br />At runtime, the following occurs:</para>
      <para>If <legacyBold>Input XML instance is of type “Email”</legacyBold>: Only the “subject” element is created in the output XML instance with the value copied from input XML.</para>
      <para>If <legacyBold>Input XML instance is of type “MassEmailMessage”</legacyBold>: The “toAddresses” element is created in the output XML instance with the value copied from “targetObjectIds” in input XML.</para>
      <para>If <legacyBold>Input XML instance is of type “SingleEmailMessage”</legacyBold>: The “toAddresses” element is created in the output XML instance with the value copied from “toAddresses” in input XML. The “targetObjectIds” in input XML is ignored.</para>
      <alert class="important">
        <para>The xsi:type is not assigned to a Target node based on a fixed or default value in the schema.</para>
      </alert>
    </content>
    <sections>
      <section>
        <title>Example: Links under Same Element in Base and Derived Types</title>
        <content>
          <para>In this example, there is a “Mileage” element that exists in the “Vehicle” base type, exists in the “Car” Derived Type, and also exists in the “Truck” Derived Type:</para>
          <mediaLink>
            <image xlink:href="e482083d-c383-4eb6-bc59-02a5268d28c7" />
          </mediaLink>
          <para>
            <br />The following table shows sample Input XML. When processed by this <token>transform</token>, it shows the Output XML:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Input XML</para>
                </TD>
                <TD>
                  <para>Output XML</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <code>
&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle&gt;
       &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyVehicle&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns0:Truck"&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;4&lt;/VolumeCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyTruck&gt;
      &lt;VolumeCapacity&gt;10&lt;/VolumeCapacity&gt;
   &lt;/MyTruck&gt;

&lt;/ns1:Root&gt;</code>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns0:Car"&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyCar&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyCar&gt;

&lt;/ns1:Root&gt;</code>
                  <para />
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>Example: Links under Different Elements in Base and Derived Types</title>
        <content>
          <para>In this example, there is a “Mileage” element in the “Vehicle” base type and other links under the “Car” and “Truck” Derived Types:</para>
          <mediaLink>
            <image xlink:href="c91fb100-26f2-4679-947b-0824713cb6fd" />
          </mediaLink>
          <para>
            <br />The following table shows sample Input XML. When processed by this <token>transform</token>, it shows the Output XML:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Input XML</para>
                </TD>
                <TD>
                  <para>Output XML</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <code>
&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle&gt;
       &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyVehicle&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns0:Truck"&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;4&lt;/VolumeCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyTruck&gt;
      &lt;VolumeCapacity&gt;4&lt;/VolumeCapacity&gt;
   &lt;/MyTruck&gt;

&lt;/ns1:Root&gt;</code>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns0:Car"&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyCar&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyCar&gt;

&lt;/ns1:Root&gt;</code>
                  <para />
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
      <section>
        <title>Example: Links under Different nodes in Derived Types</title>
        <content>
          <para>In this example, there are links under the “Car” and “Truck” Derived Types:</para>
          <mediaLink>
            <image xlink:href="f0f8d6c0-13b8-483d-93a5-b9915ce035f4" />
          </mediaLink>
          <para>
            <br />The following table shows sample Input XML. When processed by this <token>transform</token>, it shows the Output XML:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Input XML</para>
                </TD>
                <TD>
                  <para>Output XML</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <code>
&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle&gt;
       &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes" /&gt;</code>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns0:Truck"&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;4&lt;/VolumeCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyTruck&gt;
      &lt;VolumeCapacity&gt;4&lt;/VolumeCapacity&gt;
   &lt;/MyTruck&gt;

&lt;/ns1:Root&gt;</code>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;ns0:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns0:Car"&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns0:Root&gt;</code>
                  <para />
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyCar&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyCar&gt;

&lt;/ns1:Root&gt;</code>
                  <para />
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_NToD">
    <title>Scenario: Links from Normal Type to Derived Type</title>
    <content>
      <para>In a <token>transform</token>, the Source schema has a Normal Type and the Target schema has a Derived Type. The “xsi:type” value in the input XML is based on the links. The "xsi:type" in the output XML instance is automatically stamped based on the incoming links. </para>
      <para>In the following example, the Source schema has Normal Type nodes and the Target schema has Multi Type nodes. In the Target schema, “Email” is the base and “MassEmailMessage” is a Derived Type of “Email”:</para>
      <mediaLink>
        <image xlink:href="35bef9fe-0eeb-4a28-b372-83a6e351fb10" />
      </mediaLink>
      <para>
        <br />At runtime, the "sendEmail" xsi:type is set to "MassEmailMessage" since the links are drawn to nodes under the "MassEmailMessage" node. The “subject” and “targetObjectIds” values are copied from the corresponding fields in the input XML.</para>
      <alert class="important">
        <para>The xsi:type is not assigned to a Target node based on a fixed or default value in the schema.</para>
      </alert>
    </content>
    <sections>
      <section>
        <title>Example: Link from Normal Type to Multi Type</title>
        <content>
          <para>When a Normal Type node in the Source schema has only one link to a Multi Type node on the Target schema, the type is not set in the output. In this example, the goal is to create “MyVehicle” and not do any additional links. “MyVehicle” in the Source is linked to “MyVehicle” in the Target:</para>
          <mediaLink>
            <image xlink:href="3a50f9dc-566f-4056-b70f-e695951d6198" />
          </mediaLink>
          <para>
            <br />The following table shows sample Input XML. When processed by this Transform, it shows the Output XML:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Input XML</para>
                </TD>
                <TD>
                  <para>Output XML</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyVehicle&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkService1.Vehicle_SimpleTypes" xmlns:ns1="http://BizTalkServiceArtifacts1.VehicleDerivedType"&gt;

   &lt;MyVehicle&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
              </tr>
            </tbody>
          </table>
          <para>The type (xsi:type) is not set to “MyVehicle” in the output XML instance. According to XML schema standards, if the type (xsi:type) is not explicitly mentioned for any element that has Derived Typess, then it is considered as a Base Type element.</para>
        </content>
      </section>
      <section>
        <title>Example: Links from Normal Type to Derived Types using MapEach</title>
        <content>
          <para>In this example, “MyVehicle, “MyCar”, and “MyTruck” are Normal Types in the Source schema. The minOccurs is “0” and maxOccurs is “unbounded” for “MyVehicle”, “MyTruck”, and “MyCar”.</para>
          <para>The Target schema has a “Vehicle” base type, a “Car” Derived Type, and a “Truck” Derived Type. “MyVehicle” is an element of type “Vehicle” under the root node. The minOccurs is “0” and maxOccurs is “unbounded” for “MyVehicle”:</para>
          <mediaLink>
            <image xlink:href="46718b07-a18e-4f34-9c8f-4c123c2efcaf" />
          </mediaLink>
          <para>
            <br />The following table shows sample Input XML. When processed by this Transform, it shows the Output XML:</para>
          <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>Input XML</para>
                </TD>
                <TD>
                  <para>Output XML</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyVehicle&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkService1.Vehicle_SimpleTypes" xmlns:ns1="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle/&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyCar&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;5&lt;/SeatingCapacity&gt;
   &lt;/MyCar&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkService1.Vehicle_SimpleTypes" xmlns:ns1="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns1:Car"&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;5&lt;/SeatingCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyTruck&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;1000&lt;/VolumeCapacity&gt;
   &lt;/MyTruck&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkService1.Vehicle_SimpleTypes" xmlns:ns1="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns1:Truck"&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;1000&lt;/VolumeCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:ns1="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyVehicle&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;
   &lt;MyCar&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;5&lt;/SeatingCapacity&gt;
   &lt;/MyCar&gt;
   &lt;MyTruck&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;1000&lt;/VolumeCapacity&gt;
   &lt;/MyTruck&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkService1.Vehicle_SimpleTypes" xmlns:ns1="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle/&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;
   &lt;MyVehicle xsi:type="ns1:Car"&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;5&lt;/SeatingCapacity&gt;
   &lt;MyVehicle xsi:type="ns1:Truck"&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;1000&lt;/VolumeCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
              </tr>
              <tr>
                <TD>
                  <code>&lt;ns0:Root xmlns:ns0="http://BizTalkService1.Vehicle_SimpleTypes"&gt;

   &lt;MyVehicle&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;
   &lt;MyVehicle&gt;
      &lt;Mileage&gt;12&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;
   &lt;MyCar&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyCar&gt;
   &lt;MyCar&gt;
      &lt;Mileage&gt;18&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyCar&gt;
   &lt;MyTruck&gt;
      &lt;Mileage&gt;6&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;800&lt;/VolumeCapacity&gt;
   &lt;/MyTruck&gt;
   &lt;MyTruck&gt;
      &lt;Mileage&gt;5&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;1000&lt;/VolumeCapacity&gt;
   &lt;/MyTruck&gt;

&lt;/ns0:Root&gt;</code>
                </TD>
                <TD>
                  <code>&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;ns1:Root xmlns:ns0="http://BizTalkService1.Vehicle_SimpleTypes" xmlns:ns1="http://BizTalkServiceArtifacts1.VehicleDerivedType" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;

   &lt;MyVehicle xsi:type="ns1:Vehicle"&gt;
      &lt;Mileage&gt;10&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;
   &lt;MyVehicle xsi:type="ns1:Vehicle"&gt;
      &lt;Mileage&gt;12&lt;/Mileage&gt;
   &lt;/MyVehicle&gt;
   &lt;MyVehicle xsi:type="ns1:Car"&gt;
      &lt;Mileage&gt;15&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyVehicle&gt;
   &lt;MyVehicle xsi:type="ns1:Car"&gt;
      &lt;Mileage&gt;18&lt;/Mileage&gt;
      &lt;SeatingCapacity&gt;4&lt;/SeatingCapacity&gt;
   &lt;/MyVehicle&gt;
   &lt;MyVehicle xsi:type="ns1:Truck"&gt;
      &lt;Mileage&gt;6&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;800&lt;/VolumeCapacity&gt;
   &lt;/MyVehicle&gt;
   &lt;MyVehicle xsi:type="ns1:Truck"&gt;
      &lt;Mileage&gt;5&lt;/Mileage&gt;
      &lt;VolumeCapacity&gt;1000&lt;/VolumeCapacity&gt;
   &lt;/MyVehicle&gt;

&lt;/ns1:Root&gt;</code>
                </TD>
              </tr>
            </tbody>
          </table>
        </content>
      </section>
    </sections>
  </section>
  <section address="BKMK_DToD">
    <title>Scenario: Links from Derived Type to Derived Type</title>
    <content>
      <para>In a <token>transform</token>, the Source schema has a Derived Type and the Target schema has a Derived Type. This scenario is similar to “Derived Type to Normal Type” scenario. Links from a Derived Type are only evaluated when the “xsi:type” value in the input XML message matches the Derived Type.</para>
      <alert class="important">
        <para>The xsi:type is not assigned to a Target node based on a fixed or default value in the schema.</para>
      </alert>
    </content>
    <sections>
      <section>
        <title>Example: Source and Target schemas have Derived Types</title>
        <content>
          <para>In this example, the Source and Target schemas both have Derived Types. The Source schema has a “messages” object that has three Equivalent types - “Email”, “MassEmailMessage”, and “SingleEmailMessage”. The Target schema has two Equivalent types – “Email” and “MassEmail”:</para>
          <mediaLink>
            <image xlink:href="a1e0999f-284c-41fc-8946-c6e85dc059cd" />
          </mediaLink>
          <para>
            <br />At runtime, the following occurs: </para>
          <para>If <legacyBold>the “messages” element in the input XML instance is of type “Email”</legacyBold>: the “sendEmail” element of type “Email” (xsi:type=“Email”) is created in the output XML instance and the “subject” element value is copied from “subject” in the Source schema.</para>
          <para>If <legacyBold>the “messages” element in the input XML instance is of type “MassEmailMessage”</legacyBold>: the “sendEmail” element of type “MassEmail” (xsi:type=“MassEmail”) is created in the output XML instance. The “ToAddresses” element value is copied from “whatIds” in the Source schema.</para>
          <para>If <legacyBold>the “messages” element in the input XML instance is of type “SingleEmailMessage”</legacyBold>: no element is created in the output XML instance.</para>
        </content>
      </section>
    </sections>
  </section>
  <relatedTopics>
    <link xlink:href="5a028e9a-b0e7-4d44-a121-38b876f8020f">Standard XSD constructs are supported</link>
  </relatedTopics>
</developerConceptualDocument>