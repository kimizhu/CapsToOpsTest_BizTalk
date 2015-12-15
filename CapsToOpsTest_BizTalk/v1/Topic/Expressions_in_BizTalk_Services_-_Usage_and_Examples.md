---
description: na
keywords: na
pagetitle: Expressions in BizTalk Services - Usage and Examples
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 567064b1-5b6d-4209-baf1-c730279f8d04
---
# Expressions in BizTalk Services - Usage and Examples
Lists the Expression [!INCLUDE[mapop](/Token/mapop_md.md)]s in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)].

## Expressions Map Operators

|[!INCLUDE[mapop](/Token/mapop_md.md)] <br /> <br />|Description <br /> <br />|Parameters <br /> <br />|Output <br /> <br />|
|-----------------------------------------|---------------|--------------|----------|
|Arithmetic Expression <br /> <br />|Evaluates a mathematical expression using inputs and constants. Arithmetic Expressions consists of the following operators: <br /> <br /><ul><li>Addition </li><li>Subtraction </li><li>Multiplication </li><li>Division </li><li>Modulo </li><li>Absolute Value </li><li>Maximum </li><li>Minimum </li><li>Round </li><li>Square Root </li> </ul>|Can have 0 to 100 optional input parameters: <br /> <br />*Input* <br /> <br />A numeric value. <br /> <br />*Arithmetic Expression* <br /> <br />A mathematical expression defined using the inputs and constants. **Note:** The maximum length for an expression is 1024 characters. <br />|A numeric value that is the result of the computation. <br /> <br />See [Arithmetic Expression Examples: BizTalk Services](/Topic/Arithmetic_Expression_Examples__BizTalk_Services.md). <br /> <br />|
|Logical Expression <br /> <br />|Evaluates a condition and outputs the Boolean value of the evaluation. Logical Expression consists of the following operators: <br /> <br /><ul><li>Relational Operators: <br /> <br />   &gt; <br /> <br />   &lt; <br /> <br />   &gt;= <br /> <br />   &lt;= <br /> <br />   == <br /> <br />   != </li><li>Logical Negation (!) </li><li>Conditional AND (&amp;&amp;) <br /> <br />   Conditional OR (&#124;&#124;) </li> </ul>|Can have 0 to 100 optional input parameters: <br /> <br />*Input* <br /> <br />Can be a numeric value, string value or Boolean value. <br /> <br />*Logical Expression* <br /> <br />An expression defined using the inputs and constants that evaluate to a Boolean value. **Note:** The maximum length for an expression is 1024 characters. <br />|True is returned if the Logical Expression returns true. Otherwise, False is returned. <br /> <br />See [Logical Expression Examples: BizTalk Services](/Topic/Logical_Expression_Examples__BizTalk_Services.md). <br /> <br />|
|If-Then-Else Expression <br /> <br />|Evaluates a statement that results in one of two possible outputs. <br /> <br />|Can have 0 to 100 optional input parameters: <br /> <br />*Input* <br /> <br />Can be a numeric value, string value or Boolean value. <br /> <br />*Condition* <br /> <br />An expression defined using the inputs and constants. <br /> <br />*Then Value* <br /> <br />If statement or expression is true, this value is used. <br /> <br />*Else Value* <br /> <br />If statement or expression is false, this value is used. **Note:** The maximum length for an expression is 1024 characters. <br />|The result is based on a true or false evaluation of the conditional expression. <br /> <br />If true, the *Then Value* is used. If false, the *Else Value* is used. <br /> <br />See [If-Then-Else Expression Example: BizTalk Services](/Topic/If-Then-Else_Expression_Example__BizTalk_Services.md). <br /> <br />|
|Conditional Assignment <br /> <br />|Returns a value from one of two input parameters. If the first input value is True, then a node is created in the output document with the second input value. If the first input value is False, then the corresponding node is not created in the output document. <br /> <br />|Requires exactly two input parameters: <br /> <br />*Condition* <br /> <br />An expression that results in a Boolean value. Can be one of the following: <br /> <br /><ul><li>Link from tree node </li><li>Link from a [!INCLUDE[mapop](/Token/mapop_md.md)] </li> </ul>*Assign Value* <br /> <br />The value assigned to the destination node if the condition is true. **Note:** This [!INCLUDE[mapop](/Token/mapop_md.md)] can only be connected to a destination tree node. <br />|If the *Condition* value is "true", then a node is created with the *Assign Value* input value. <br /> <br />See [Conditional Assignment Example: BizTalk Services](/Topic/Conditional_Assignment_Example__BizTalk_Services.md). <br /> <br />|
The following table lists additional functions that can be used with any [!INCLUDE[mapop](/Token/mapop_md.md)]:

|Function <br /> <br />|Expression <br /> <br />|Description <br /> <br />|
|------------|--------------|---------------|
|Exists <br /> <br />|Exists(*Source_Node_Name*) <br /> <br />|Requires a single input that is the element name in the source document. If the element exists, True is returned. Otherwise, False is returned. <br /> <br />|
|IsDate <br /> <br />|IsDate(*Input1*) <br /> <br />|Requires a single input of the type string. The DateTime.TryParse() method is used to parse the input into a DateTime object. If the input is parsed successfully, True is returned. Otherwise, False is returned. <br /> <br />|
|IsEmpty <br /> <br />|IsEmpty(*Input1*) <br /> <br />|Requires a single input of the type string. If the string is null or empty, True is returned. Otherwise, False is returned. If the input is not a string object, True is returned. <br /> <br />|
|IsNil <br /> <br />|IsNil(*Source_Node_Name*) <br /> <br />|Requires a single argument that is the element name in the source document. If the element exists and xsi:nil is set to True, then True is returned. Otherwise, False is returned. <br /> <br />|
|IsNumber <br /> <br />|IsNumber(*Input1*) <br /> <br />|Requires a single input of the type string. The Double.TryParse() method is used to parse the input into a double. If the input is parsed successfully, True is returned. Otherwise, False is returned. **Note:** The comma “,” is supported as the thousands separator and the period “.” is supported as a decimal point. <br />|
> [!IMPORTANT]
> All [!INCLUDE[mapop](/Token/mapop_md.md)] and functions can be used within other [!INCLUDE[mapop](/Token/mapop_md.md)] and functions *except* Exists and IsNil. Exists and IsNil point to a single node in the source document.

## Error and Data Handling
[!INCLUDE[af_integration](/Token/af_integration_md.md)] provides the ability to configure how an error is handled and how an empty or null node is handled. The error handling behavior of the following **Expression**[!INCLUDE[mapop](/Token/mapop_md.md)]s is configurable:

- **Logical Expression**

- **Arithmetic Expression**

- **If-Then-Else Expression**

Steps:

1. Open a **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]** or the **BizTalk Service Artifacts** project in [!INCLUDE[vs_current_short](/Token/vs_current_short_md.md)].

2. Double-click a [!INCLUDE[transform](/Token/transform_md.md)] (.trfm) to open the [!INCLUDE[transform](/Token/transform_md.md)] Designer.

3. In the [!INCLUDE[transform](/Token/transform_md.md)] toolbar, click **Settings**.

**Error Handling tab**

In the **Error Handling** tab, the following **Expression**[!INCLUDE[mapop](/Token/mapop_md.md)]s have two **Behavior** options:

- **Logical Expression**:

   - **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and the error is then sent back to the client that sent the message.

   - **Output default value false**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, False is returned as the output.

- **Arithmetic Expression**:

   - **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and the error is then sent to the client that sent the message.

   - **Output default value NaN**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, NaN (Not a Number) is returned as the output.

   - **Output default value 0**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, zero (0) is returned as the output.

- **If-Then-Else Expression**:

   - **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and the error is then sent back to the client that sent the message.

   - **Output Null/Zero/False based on type of output**: If the [!INCLUDE[mapop](/Token/mapop_md.md)] fails, Null/Zero/False is returned as the output based on type of output.

**Null/Empty Data Handling tab**

In the **Null/Empty Data Handling** tab, there are three options:

- **Consider empty nodes in cumulative operations**: By default, this is not checked. When not checked, no empty nodes are included in the iteration. When checked, all nodes, including empty nodes, are included in the iteration.

   EXAMPLE: There is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. When **Consider empty nodes in iterations** is not checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] returns a value of seven. When **Consider empty nodes in iterations** is checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] returns a value of 10.

- **Consider empty nodes in iterations**: By default, this is not checked. When not checked, no empty nodes are included in the iteration. When checked, all nodes, including empty nodes, are included in the iteration.

   EXAMPLE: there is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. When **Consider empty nodes in iterations** is not checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] iterates seven times for the non-empty nodes. As a result, seven &lt;record&gt; nodes are generated in the Target. When **Consider empty nodes in iterations** is checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] iterates 10 times for all nodes, including the empty nodes. As a result, 10 &lt;record&gt; nodes are generated in the Target.

- **Target Node Generation**: If empty nodes are configured to be considered, you choose to generate an empty node in the output or to not generate an empty node in the output. Specifically:

   - Do not generate empty nodes: Default option.

   - Generate empty nodes

   EXAMPLE: There is a document with 10 &lt;record&gt; nodes. Three of these &lt;record&gt; nodes are empty. **Consider empty nodes in cumulative operations** or **Consider empty nodes in iterations** are not checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] iterates seven times for the non-empty nodes. As a result, seven &lt;record&gt; nodes are generated in the Target. When **Consider empty nodes in iterations** is checked, the [!INCLUDE[mapop](/Token/mapop_md.md)] iterates 10 times for all nodes, including the empty nodes. As a result, 10 &lt;record&gt; nodes are generated in the Target.

## In This Section
[Arithmetic Expression Examples: BizTalk Services](/Topic/Arithmetic_Expression_Examples__BizTalk_Services.md)

[Logical Expression Examples: BizTalk Services](/Topic/Logical_Expression_Examples__BizTalk_Services.md)

[If-Then-Else Expression Example: BizTalk Services](/Topic/If-Then-Else_Expression_Example__BizTalk_Services.md)

[Conditional Assignment Example: BizTalk Services](/Topic/Conditional_Assignment_Example__BizTalk_Services.md)

## Additional [!INCLUDE[mapop](/Token/mapop_md.md)]s
[String Map Operations - Usage and Examples](/Topic/String_Map_Operations_-_Usage_and_Examples.md)

[Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md)

[List Map Operations - Usage and Examples](/Topic/List_Map_Operations_-_Usage_and_Examples.md)

[Cumulative Map Operations - Usage and Examples](/Topic/Cumulative_Map_Operations_-_Usage_and_Examples.md)

[Date &#47; Time Map Operations - Usage and Examples](/Topic/Date_/_Time_Map_Operations_-_Usage_and_Examples.md)

[Miscellaneous Map Operations - Usage and Examples](/Topic/Miscellaneous_Map_Operations_-_Usage_and_Examples.md)

## See Also
[Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md)

