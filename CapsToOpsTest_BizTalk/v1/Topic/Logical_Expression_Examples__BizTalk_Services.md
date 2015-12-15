---
description: na
keywords: na
pagetitle: Logical Expression Examples: BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02e5e71f-3e13-4358-88be-6e9f1ba4f79a
---
# Logical Expression Examples: BizTalk Services
Lists Logical Expression Examples in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)].

## Logical Expression Examples
All boolean input values are based on Boolean Literals to represent string values of the CLR System.Boolean type. They are written as **True** and **False**.

All string input values are based on String Literals to represent string values of the CLR System.String type. There are two types of string literals:

- Regular string literals

- Verbatim string literals

Regular string literals are written as a sequence of characters enclosed in quotation marks (“ “). The regular string literals supported by C# are also supported by the [!INCLUDE[transform](/Token/transform_md.md)] parser *except* the escape sequence (\x). The escape sequence (\x) is not supported.

Verbatim string literals are written as a sequence of characters enclosed in quotation marks (“ “) and prefixed with the @ symbol. The verbatim string literals supported by C# are also supported by the [!INCLUDE[transform](/Token/transform_md.md)] parser.

The [Double.TryParse()](http://go.microsoft.com/fwlink/p/?LinkId=228961) method is used to verify that a boolean or string literal value is a valid double value. If not, the argument is converted to a double using the [Convert.ToDouble()](http://go.microsoft.com/fwlink/p/?LinkId=228962) method.

The [String.Compare()](http://go.microsoft.com/fwlink/p/?LinkId=228963) method is used to compare string values. Uppercase letters are assumed to occur before lowercase letters. For specific details on how string comparison works, go to [String.Compare(String, String, StringComparison)](http://go.microsoft.com/fwlink/p/?LinkId=228964).

Logical expression reminders:

- String literals must use quotations marks.

- When expressions are being evaluated, Conditional AND (&amp;&amp;) has a higher precedence than Conditional OR (||).

- Use parenthesis to control the order. For example, using the Conditional OR (||) within parenthesis allows this part of the expression to be evaluated first.

### Sample Expressions

### Relational Operators: &lt;, &gt;, &lt;=, &gt;=
Requires two inputs of the type double. Operator behavior:

1. An attempt is made to convert the inputs to double. If **both** inputs are successfully converted to double, the comparison is made and the appropriate Boolean value is returned. If the conversion to double fails for both inputs, the next check is performed.

2. A check is done to confirm that both values are of type string. If **both** values are of type string, an [Ordinal StringComparison](http://go.microsoft.com/fwlink/p/?LinkId=228965) is performed and the appropriate Boolean value is returned. If **both** values are not of type string, False is returned.

Sample expressions using the following input values:

|||
|-|-|
|*Input1* <br /> <br />|ab123.456 <br /> <br />|
|*Input2* <br /> <br />|78.9 <br /> <br />|
|*Input3* <br /> <br />|-123.11 <br /> <br />|
|*Input4* <br /> <br />|“MSFT” <br /> <br />|
|*Input5* <br /> <br />|“Redmond” <br /> <br />|

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|*Input1*&gt;=*Input3* <br /> <br />|**False** <br /> <br />*Input1* fails the conversion to double. <br /> <br />|
|*Input2*&lt;*Input3* <br /> <br />|78.9 &lt; (-123.11) = **False** <br /> <br />The StringComparison is not performed since the input values are numeric. <br /> <br />|
|*Input4*&lt;*Input5* <br /> <br />|“MSFT” &lt; “Redmond” = **True** <br /> <br />The StringComparison is performed since the input values are both string. M occurs before R in the alphabet so the value is True. <br /> <br />|
|*Input5*&lt;=*Input2* <br /> <br />|**False** <br /> <br />*Input5* fails the conversion to double. <br /> <br />|

### Equality Operators: == and !=
Both operators require two inputs of the type bool. == operator behavior:

1. An attempt is made to convert the inputs to bool. If **both** inputs are successfully converted to bool, the comparison is made and the appropriate Boolean value is returned. If the conversion to bool fails for both inputs, the next step is performed.

2. An attempt is made to convert the inputs to double. If **both** inputs are successfully converted to double, the comparison is made and the appropriate Boolean value is returned. If the conversion to double fails for both inputs, the next check is performed.

3. A check is done to confirm that both values are of type string. If **both** values are of type string, an [Ordinal StringComparison](http://go.microsoft.com/fwlink/p/?LinkId=228965) is performed and the appropriate Boolean value is returned. If **both** values are not of type string, False is returned.

The ‘!=’ operator is to return the logical negation of the ‘==’ operator. For example, if a comparison returns True, != returns False.

Sample expressions using the following input values:

|||
|-|-|
|*Input1* <br /> <br />|ab123.456 <br /> <br />|
|*Input2* <br /> <br />|78.9 <br /> <br />|
|*Input3* <br /> <br />|-123.11 <br /> <br />|
|*Input4* <br /> <br />|“MSFT” <br /> <br />|
|*Input5* <br /> <br />|“Redmond” <br /> <br />|

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|*Input1*==*Input3* <br /> <br />|**False** <br /> <br />*Input1* fails the conversion to bool. <br /> <br />|
|*Input2*==*Input3* <br /> <br />|78.9 == (-123.11) = **False** <br /> <br />*Input2***and***Input3* fail the conversion to bool. <br /> <br />*Input2***and***Input3* succeed the conversion to double. The comparison results in False. <br /> <br />|
|*Input4*!=*Input5* <br /> <br />|“MSFT” != “Redmond” = **True** <br /> <br />*Input4***and***Input5* fail the conversion to bool. <br /> <br />*Input4***and***Input5* fail the conversion to double. <br /> <br />*Input4***and***Input5* are of type string so an [Ordinal String Comparison](http://go.microsoft.com/fwlink/?LinkId=228965) is performed. <br /> <br />|
|*Input5*!=*Input2* <br /> <br />|**False** <br /> <br />*Input5* fail the conversion to bool. <br /> <br />|

### Logical Negation: !
Requires a single input of the type bool. Operator behavior:

1. A check is done to determine if the input is of type bool **or** if the input is of type string that can be converted to bool. If the check succeeds, the logical negation of the input is returned. If the check fails, the next step is performed. Note that the input is not converted to bool.

2. The input value is converted to double. If the conversion succeeds **and** the value is zero, True is returned. If the conversion succeeds **and** the value is non-zero, False is returned.

3. Lastly, False is returned

> [!NOTE]
> After the value is extracted at every step listed above, the negation is already listed.

Sample expressions using the following input values:

|||
|-|-|
|*Input1* <br /> <br />|ab123.456 <br /> <br />|
|*Input2* <br /> <br />|78.9 <br /> <br />|
|*Input3* <br /> <br />|-123.11 <br /> <br />|
|*Input4* <br /> <br />|“MSFT” <br /> <br />|
|*Input5* <br /> <br />|“Redmond” <br /> <br />|

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|!*Input1* <br /> <br />|**False** <br /> <br />*Input1* fails the bool value check and fails the conversion to double. So, False is returned. <br /> <br />|
|!*Input2* <br /> <br />|**False** <br /> <br />*Input2* is already a double value and is non-zero. So False is returned. <br /> <br />|
|!*Input3* <br /> <br />|**False** <br /> <br />*Input3* is already a double value and is non-zero. So False is returned. <br /> <br />|
|!*Input5* <br /> <br />|**False** <br /> <br />*Input5* fails the bool value check and fails the conversion to double. So, False is returned. <br /> <br />|

### Conditional Logical Operators: &amp;&amp; and ||
Requires two inputs of the type bool. Operator behavior:

1. A check is done to determine if the inputs are of type bool **or** if the inputs are of type string that can be converted to bool. If the check succeeds, True is returned. If the check fails, the next step is performed.

2. The input values are converted to double. If the conversion succeeds **and** the value is non-zero, True is returned. If the conversion succeeds **and** the value is zero, False is returned. If the conversion to double fails, the next check is performed.

3. A check is done to confirm that the values are of type string. If the values are of type string **and** the string values are not null, True is returned.

4. Lastly, False is returned.

Sample expressions using the following input values:

|||
|-|-|
|*Input1* <br /> <br />|City <br /> <br />|
|*Input2* <br /> <br />|State <br /> <br />|
|*Input3* <br /> <br />|Zip <br /> <br />|
|*Logical Expression* <br /> <br />|City == “Redmond” &#124;&#124; State == “WA” &amp;&amp; Zip == 98052 <br /> <br />|

|Sample Data <br /> <br />|Result <br /> <br />|
|---------------|----------|
|City is Redmond, State is WA and Zip is 98052 <br /> <br />|**True** <br /> <br />The (State == “WA” &amp;&amp; Zip == 98052) sub-expression will return True. The (City == “Redmond”) sub-expression will return True. Therefore, the expression will evaluate to True. <br /> <br />|
|City is Redmond, State is WA and Zip is 12345 <br /> <br />|**True** <br /> <br />The (State == “WA” &amp;&amp; Zip == 98052) sub-expression will return False. The (City == “Redmond”) sub-expression will return True. Therefore, the expression will evaluate to True. <br /> <br />|
|City is Redmond, State is *null* and Zip is *null* <br /> <br />|**True** <br /> <br />The (State == “WA” &amp;&amp; Zip == 98052) sub-expression will return False. The (City == “Redmond”) sub-expression will return True. Therefore, the expression will evaluate to True. <br /> <br />|
|City is Seattle, State is WA and Zip is 98052 <br /> <br />|**False** <br /> <br />The (State == “WA” &amp;&amp; Zip == 98052) sub-expression will return True. The (City == “Redmond”) sub-expression will return False. Therefore, the expression will evaluate to False. <br /> <br />|
|City is Seattle, State is NC and Zip is 98052 <br /> <br />|**False** <br /> <br />The (State == “WA” &amp;&amp; Zip == 98052) sub-expression will return False. The (City == “Redmond”) sub-expression will return False. Therefore, the expression will evaluate to False. <br /> <br />|

## Error and Data Handling
If an error occurs with a **Logical Expression**, by default, the entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. This error handling behavior is configurable. See **Error and Data Handling** at [Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md).

## See Also
[Arithmetic Expression Examples: BizTalk Services](/Topic/Arithmetic_Expression_Examples__BizTalk_Services.md)
[If-Then-Else Expression Example: BizTalk Services](/Topic/If-Then-Else_Expression_Example__BizTalk_Services.md)
[Conditional Assignment Example: BizTalk Services](/Topic/Conditional_Assignment_Example__BizTalk_Services.md)
[Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md)

