---
description: na
keywords: na
pagetitle: String Map Operations - Usage and Examples
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a6b1c171-1871-4ef4-923b-d109104ddf14
---
# String Map Operations - Usage and Examples

## String [!INCLUDE[mapop](/Token/mapop_md.md)]s
The following table lists the String [!INCLUDE[mapop](/Token/mapop_md.md)]s in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)]:

|Map Operator <br /> <br />|Description <br /> <br />|Parameters <br /> <br />|Output <br /> <br />|
|----------------|---------------|--------------|----------|
|String Concatenate <br /> <br />|Concatenates strings in the order listed. <br /> <br />|Requires at least one input parameter. No maximum limit on the number input parameters: <br /> <br />*Input_1:* <br /> <br />Required. A string that is concatenated to. <br /> <br />*Input_n:* <br /> <br />Optional. A string that is concatenated with the previous string input. **Note:** Strings are concatenated in the order listed. <br />|A string that concatenated the input strings in the order specified. <br /> <br />For example, when using “**1 Microsoft Way**” and “**Redmond WA**” as input strings, the result is “**1 Microsoft WayRedmond WA**”. **Important:** There is no trailing space at the end of the first string or a leading space at the beginning of the second string. As a result, there is no space between “**Way**” and “**Redmond**”. <br />|
|String Find <br /> <br />|Returns the starting position of a substring. <br /> <br />|Requires exactly two input parameters: <br /> <br />*Input string:* <br /> <br />Required. A string that is being searched through. <br /> <br />*Search String* <br /> <br />Required. A string that is being searched for. <br /> <br />|A numeric value **starting at 1** that is the **starting** position of the first character in the substring. Zero (0) indicates that the substring was not found. <br /> <br />For example, searching for the “**Redmond**” substring within the “**1 Microsoft Way Redmond WA**” input string returns a numeric value of 17. <br /> <br />|
|String Left <br /> <br />|Retrieves a specified number of characters, starting with the leftmost character. <br /> <br />|Requires exactly two input parameters: <br /> <br />*Input string:* <br /> <br />Required. A string to retrieve a specified number of its leftmost characters. <br /> <br />*Number of Characters:* <br /> <br />Required. A numeric value that represents the number of leftmost characters to retrieve. <br /> <br />|A string that contains the specified number of leftmost characters. <br /> <br />For example, using “**Redmond WA**” as an input string and 3 for the *Number of Characters*, the result is “**Red**”. <br /> <br />|
|Lowercase <br /> <br />|Converts any uppercase characters within a string to lowercase. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input string:* <br /> <br />Required. A string to convert any uppercase characters to lowercase. <br /> <br />|Any uppercase characters within the string are now in lowercase. <br /> <br />For example, an input string of “**Redmond WA**” is returned as “**redmond wa**”. <br /> <br />|
|String Right <br /> <br />|Retrieves a specified number of characters, starting with the rightmost character. <br /> <br />|Requires exactly two input parameters: <br /> <br />*Input string:* <br /> <br />Required. A string to retrieve a specified number of its rightmost characters. <br /> <br />*Number of Characters* <br /> <br />Required. A numeric value that represents the number of rightmost characters to retrieve. <br /> <br />|A string that contains the specified number of rightmost characters. <br /> <br />For example, using “**Redmond WA**” as an input string and 3 for the *Number of Characters*, the result is “ **WA**”. **Important:** There is a space between “**Redmond**” and “**WA**”. As a result, the space is displayed in the output. <br />|
|Size <br /> <br />|Retrieves the length of a string. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input string:* <br /> <br />Required. A string to determine the length. <br /> <br />|A numeric value that is the length of the string. <br /> <br />For example, “**Redmond WA**” as an input string returns a numeric value of 10. <br /> <br />|
|String Extract <br /> <br />|Extracts a substring by specifying the start and end positions. <br /> <br />|Requires exactly three input parameters: <br /> <br />*Input string* <br /> <br />Required. A string to extract from. <br /> <br />*Start Index* <br /> <br />Required. A numeric value **starting at 1** that is the starting character of the substring to be extracted. <br /> <br />*End Index* <br /> <br />Required. A numeric value **starting at 1** that is the ending character of the substring to be extracted. <br /> <br />|A string that contains the extracted substring. <br /> <br />For example, a *Start Index* of 2 and *End Index* of 5 of the “**Redmond WA**” input string returns “**edmo**”; where “**e**” is the second character, “**d**” is the third character, “**m**” is the fourth character and “**o**” is the fifth character. <br /> <br />An empty string is returned if the substring cannot be extracted due to incorrect *Start Index* and *End Index* values. <br /> <br />If the *Start Index***or** the *End Index* parameters exceed the size of the input string, a substring is still returned as though these parameters were set to the exact size of the string. For example, a *Start Index* of 12 and *End Index* of 5 of the “**Redmond WA**” input string would return “**Redmond WA**” because the *Start Index* exceeds the size of the input string. <br /> <br />|
|String Left Trim <br /> <br />|Removes leading white-space characters from a string. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input string* <br /> <br />Required. A string to remove leading white spaces. <br /> <br />|A string with any leading white-space characters removed. <br /> <br />For example, an input string of “ **Redmond WA**” returns “**Redmond WA**”. <br /> <br />|
|String Right Trim <br /> <br />|Removes trailing white-space characters from a string. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input string* <br /> <br />Required. A string to remove trailing white spaces. <br /> <br />|A string with any trailing white-space characters removed. <br /> <br />For example, an input string of “**Redmond WA** ” returns “**Redmond WA**”. <br /> <br />|
|Uppercase <br /> <br />|Converts any lowercase characters in a string to uppercase. <br /> <br />|Requires exactly one input parameter: <br /> <br />*Input string* <br /> <br />Required. A string to convert any lowercase characters to uppercase. <br /> <br />|Any lowercase characters within the string are now in uppercase. <br /> <br />For example, an input string of “**Redmond WA**” returns “**REDMOND WA**”. <br /> <br />|

## Error and Data Handling
[!INCLUDE[af_integration](/Token/af_integration_md.md)] provides the ability to configure how an error is handled and how an empty or null node is handled. The error handling behavior of **String** is configurable in a **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]** and the **BizTalk Service Artifacts** project. Steps:

1. Open a **[!INCLUDE[msgflow_proj](/Token/msgflow_proj_md.md)]** or a **BizTalk Service Artifacts** project in [!INCLUDE[vsprvs](/Token/vsprvs_md.md)].

2. Double-click a [!INCLUDE[transform](/Token/transform_md.md)] (.trfm) to open the [!INCLUDE[transform](/Token/transform_md.md)] Designer.

3. In the [!INCLUDE[transform](/Token/transform_md.md)] toolbar, select **Settings**.

**Error Handling tab**

In the **Error Handling** tab, **String Operations** has two **Behavior** options:

- **Fail map**: The entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. Since [!INCLUDE[transform](/Token/transform_md.md)]s are executed within a pipeline, an error occurs within the pipeline and is then sent to the user who sent the message.

- **Output default value Null**: A null string value is returned as the output. A null string behaves as an empty string behaves *except* when sorting a List. When sorting a List, null strings are considered less than empty strings.

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

## Additional [!INCLUDE[mapop](/Token/mapop_md.md)]s
[Loop Map Operations - Usage and Examples](/Topic/Loop_Map_Operations_-_Usage_and_Examples.md)

[Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md)

[List Map Operations - Usage and Examples](/Topic/List_Map_Operations_-_Usage_and_Examples.md)

[Cumulative Map Operations - Usage and Examples](/Topic/Cumulative_Map_Operations_-_Usage_and_Examples.md)

[Date &#47; Time Map Operations - Usage and Examples](/Topic/Date_/_Time_Map_Operations_-_Usage_and_Examples.md)

[Miscellaneous Map Operations - Usage and Examples](/Topic/Miscellaneous_Map_Operations_-_Usage_and_Examples.md)

## See Also
[Create a Transform or Map](/Topic/Create_a_Transform_or_Map.md)

