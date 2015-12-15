---
description: na
keywords: na
pagetitle: Arithmetic Expression Examples: BizTalk Services
search: na
ms.author: deonhe@microsoft.com
ms.date: 2015-11-27
ms.prod: azure
ms.service: biztalk-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad5ae3f4-4f3d-4308-9404-2d40da82d323
---
# Arithmetic Expression Examples: BizTalk Services
Lists Arithmetic Expression examples in [!INCLUDE[af_integration_full](/Token/af_integration_full_md.md)].

## Arithmetic Expression
All arithmetic input values are based on Numeric Literals to represent numerical values of the CLR System.Double type. The following examples demonstrate the supported numerical literals:

- 100

- 100.25

- 0.25

- .25

- 8e2, 8e+2, 8E2, 8E+2

- 1.2e8

- 1.2e-8, 1.2E-8

> [!IMPORTANT]
> The [!INCLUDE[transform](/Token/transform_md.md)] parser does not support suffixes that indicate the data type of a numeric literal. For example, using 2L to be represented as Long is not supported.

The [Double.TryParse()](http://go.microsoft.com/fwlink/p/?LinkId=228961) method is used to verify that a numeric literal value is a valid double value. If it is not a valid double value, the argument is converted to a double using the [Convert.ToDouble()](http://go.microsoft.com/fwlink/p/?LinkId=228962) method. If the conversion fails, the value is zero.

Arithmetic expression reminders:

- If an arithmetic expression has more than one operator, then **multiplication**, **division** and **modulo** are evaluated first. Then, addition and subtraction are evaluated.

- Use parenthesis to control the order. For example, adding or subtracting input values within parenthesis allows this part of the expression to be evaluated first.

- Numeric Values are not rounded unless Round is specifically used.

### Sample Expressions
The following sample expressions use the following input values:

|||
|-|-|
|*Input1* <br /> <br />|ab123.456 <br /> <br />|
|*Input2* <br /> <br />|78.9 <br /> <br />|
|*Input3* <br /> <br />|-123.11 <br /> <br />|

### Addition: +
Based off the [Expression.Add](http://go.microsoft.com/fwlink/p/?LinkId=228991) method. Requires two arguments of the type double. If a conversion to double fails, the value is zero and the operation is performed.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|*Input1*+*Input2* <br /> <br />|0 + 78.9 = **78.9** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input1*+*Input2*+*Input3* <br /> <br />|0 + 78.9 + (-123.11) = **-44.21** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input2*+*Input3* <br /> <br />|78.9 + (-123.11) = **-44.21** <br /> <br />|
|*Input1*+*Input3* <br /> <br />|0 + (-123.11) = **-123.11** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|

### Subtraction: -
Based off the [Expression.Subtract](http://go.microsoft.com/fwlink/p/?LinkId=228992) method. Requires two arguments of the type double. If a conversion to double fails, the value is zero and the operation is performed.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|*Input1*-*Input2* <br /> <br />|0 - 78.9 = **-78.9** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input1*-*Input2*-*Input3* <br /> <br />|0 - 78.9 – (-123.11) = **44.21** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input2*-*Input3* <br /> <br />|78.9 - (-123.11) = **44.21** <br /> <br />|
|*Input1*-*Input3* <br /> <br />|0 – (-123.11) = **123.11** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|(*Input1*+*Input2*)-*Input3* <br /> <br />|(0 + 78.9) – (-123.11) = **202.11** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|

### Multiplication: &#42;
Based off the [Expression.Multiply](http://go.microsoft.com/fwlink/p//?LinkId=228993) method. Requires two arguments of the type double.

If a conversion to double fails, the value is zero and the operation is performed. If both inputs are successfully converted to double, then the multiplication occurs and the value is returned. If only one of the inputs is successfully converted to double, then the value of that input is returned. If none of the inputs are successfully converted to double, then zero is returned.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|*Input1*&#42;*Input2* <br /> <br />|0 &#42; 78.9 = **78.9** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input1*&#42;*Input2*&#42;*Input3* <br /> <br />|0 &#42; 78.9 &#42; (-123.11) = **-9713.379** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input2*&#42;*Input3* <br /> <br />|78.9 &#42; (-123.11) = **-9713.379** <br /> <br />|
|*Input1*&#42;*Input3* <br /> <br />|0 &#42; (-123.11) = **-123.11** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|(*Input1*&#42;*Input2*)-*Input3*&#42;*Input2* <br /> <br />|(0 &#42; 78.9) – (-123.11) &#42; 78.9 = <br /> <br />78.9 – (-9713.379) = **9792.279** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|

### Division: /
Based off the [Expression.Divide](http://go.microsoft.com/fwlink/p/?LinkId=228994) method. Requires two arguments of the type double.

If a conversion to double fails, the value is zero and the operation is performed. If both inputs are successfully converted to double **and** the denominator value is non-zero, then the division occurs and the value is returned. Otherwise, zero is returned.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|*Input1*/*Input2* <br /> <br />|0 / 78.9 = **0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input1*/*Input2*/*Input3* <br /> <br />|0 / 78.9 / (-123.11) = **0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input2*/*Input3* <br /> <br />|78.9 / (-123.11) = **-0.6408902** <br /> <br />|
|*Input3*/*Input1* <br /> <br />|-123.11 / 0 = **0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />When the denominator is zero, the output will be zero. <br /> <br />|
|(*Input1*/*Input2*)-*Input2*/*Input3* <br /> <br />|(0 / 78.9) – (-123.11 / 78.9) = <br /> <br />0 – (-1.560329531051965) = **1.560329531051965** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|

### Modulo: %
Based off the [Expression.Modulo](http://go.microsoft.com/fwlink/p/?LinkId=228995) method. Requires two arguments of the type double.

If a conversion to double fails, the value is zero and the operation is performed. If both inputs are successfully converted to double **and** the denominator value is non-zero, then the remainder is returned. Otherwise, zero is returned.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|*Input1*%2 <br /> <br />|0 % 2 = **0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input1*+*Input2*%4 <br /> <br />|0 + 78.9 % 4 = **2.9** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />78.9 / 4 = 19.725; 19 is the quotient and 2.9 is the remainder because 78.9 = 4 &#42; 19 + 2.9 <br /> <br />|
|*Input2*%*Input1* <br /> <br />|78.9 % 0 = **0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|*Input3*%*Input2* <br /> <br />|-123.11 % 78.9 = **-44.21** <br /> <br />-123.11 / 78.9 = -1.560329531051965; -1 is the quotient and -44.21 is the remainder because -123.11 = 78.9 &#42; (-1) + (-44.21) <br /> <br />|
|(*Input1*%*Input2*)&#42;*Input2*%*Input3* <br /> <br />|(0 % 78.9) &#42; (78.9 % (-123.11)) = <br /> <br />0 &#42; (78.9) = **0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />78.9 / -123.11 = -0.6408902607424255; -0 is the quotient and 78.9 is the remainder because 78.9 = -123.11 &#42; (-0) + 78.9 <br /> <br />|

### Absolute Value: Abs(Input1)
Based off the [Math.Abs](http://go.microsoft.com/fwlink/p/?LinkId=228996) method. Requires a single argument and converts it to double. If the conversion to double is successful, it returns the absolute value of the argument. Otherwise, zero is returned.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|Abs(*Input1*) <br /> <br />|**0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|Abs(*Input2*) <br /> <br />|**78.9** <br /> <br />|
|Abs(*Input3*) <br /> <br />|**123.11** <br /> <br />|
|Abs(*Input1*)+Abs(*Input2*)+Abs(*Input3*) <br /> <br />|0 + 78.9 + 123.11 = **202.01** <br /> <br />|
|(Abs(*Input1*)&#42;Abs(*Input2*))&#42;*Input2*%Abs(*Input3*) <br /> <br />|(0&#42;78.9) &#42; 78.9 % 123.11 = <br /> <br />78.9  &#42; 78.9 % 123.11 = <br /> <br />6225.21  % 123.11 = **69.71** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />(0&#42;78.9): Remember with multiplication, if only one of the arguments can be successfully converted to double, then the value of that argument is returned. <br /> <br />6225.21 / 123.11 = 50.566241; 50 is the quotient and 69.71 is the remainder because 6225.21 = 123.11 &#42; 50 + 69.71 <br /> <br />|

### Maximum: Max(Input1, Input2)
Based off the [Math.Max](http://go.microsoft.com/fwlink/p/?LinkId=228997) method. Requires two arguments of the type double.

If both inputs are successfully converted to double, then the maximum value of the two input values is returned. If only one of the inputs is successfully converted to double, then the value of that input is returned. If none of the inputs are successfully converted to double, then zero is returned.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|Max(*Input1*, *Input2*) <br /> <br />|**78.9** <br /> <br />*Input1* fails the conversion to double so the second input value is returned. <br /> <br />|
|Max(*Input2*, *Input3*) <br /> <br />|**78.9** <br /> <br />|
|Max(*Input3*, *Input2*)+Max(*Input2*, *Input1*)+Max(*Input3*, *Input1*) <br /> <br />|78.9 + 78.9 + (-123.11) = **34.69** <br /> <br />*Input1* fails the conversion to double so the second input value is returned. <br /> <br />|
|(Max(*Input1*, *Input3*)&#42;Max(*Input2*, *Input3*))&#42; *Input2*%Abs(Max(*Input3*, *Input1*)) <br /> <br />|((-123.11) &#42; 78.9) &#42; 78.9 % 123.11 = <br /> <br />-9713.379 &#42; 78.9 % 123.11 = <br /> <br />-766385.6031 % 123.11 = **-25.8531** <br /> <br />*Input1* fails the conversion to double so the second input value is returned. <br /> <br />-766385.6031 / 123.11 = -6225.21; -6225 is the quotient and -25.8531 is the remainder because -766385.6031 = 123.11 &#42; (-6225) + (-25.8531) <br /> <br />|

### Minimum: Min(Input1, Input2)
Based off the [Math.Min](http://go.microsoft.com/fwlink/p/?LinkId=228998) method. Requires two arguments of the type double.

If both inputs are successfully converted to double, then the minimum value of the two input values is returned. If only one of the inputs is successfully converted to double, then the value of that input is returned. If none of the inputs are successfully converted to double, then zero is returned.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|Min(*Input1*, *Input2*) <br /> <br />|**78.9** <br /> <br />*Input1* fails the conversion to double so the second input value is returned. <br /> <br />|
|Min(*Input2*, *Input3*) <br /> <br />|**-123.11** <br /> <br />|
|Min(*Input3*, *Input2*)+ Min(*Input2*, *Input1*)+Min(*Input3*, *Input1*) <br /> <br />|(-123.11) + 78.9 + (-123.11) = **-167.32** <br /> <br />*Input1* fails the conversion to double so the second input value is returned. <br /> <br />|
|(Min(*Input1*, *Input3*)&#42;Min(*Input2*, *Input3*))&#42;*Input2*%Abs(Min(*Input3*, *Input1*)) <br /> <br />|((-123.11) &#42; (-123.11)) &#42; 78.9 % 123.11 = <br /> <br />15156.0721 &#42; 78.9 % 123.11 = <br /> <br />1195814.08869 % 123.11 = **46.65869** <br /> <br />*Input1* fails the conversion to double so the second input value is returned. <br /> <br />1195814.08869 / 123.11 = 9713.379; 9713 is the quotient and -46.65869 is the remainder because 1195814.08869 = 123.11 &#42; 9713 + 46.65869 <br /> <br />|

### Round: Round(Input1) or Round(Input1, numDigits)
Based off the [Math.Round](http://go.microsoft.com/fwlink/p/?LinkId=228999) method. Requires at least one argument that is converted to double and an optional second argument that must be a non-negative integer. If the conversion fails, zero is returned.

If the second argument is not provided, then the first argument is rounded to the nearest integer. If the second argument is a positive integer, then the first argument is rounded to number of digits specified in the second argument. The maximum number of digits to round is 15. Higher values for the second argument will still result in rounding to 15 places. If the second argument cannot be converted to a non-negative integer, zero is returned.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|Round(*Input1*) <br /> <br />|**0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|Round(*Input3*, *1*) <br /> <br />|**-123.1** <br /> <br />|
|Round(*Input3*, *5*) <br /> <br />|**-123.11** <br /> <br />|
|Round(*Input2*)&#42;Round(*Input3*, 1) <br /> <br />|-79 &#42; (-123.1) = **-9724.9** <br /> <br />|
|Round(*Input3*)/Round(*Input2*, 17)&#42;Round(*Input3*) <br /> <br />|123 / 78.9 &#42; 123 = <br /> <br />1.5589353 &#42; 123 = **191.74904** <br /> <br />|

### Square Root: Sqrt(Input1)
Based off the [Math.Sqrt](http://go.microsoft.com/fwlink/p/?LinkId=229000) method. Requires a single argument and converts it to double.  If the conversion is successful, the square root is returned. If the argument is a negative number, NaN is returned. If the conversion fails, zero is returned.

|Expression <br /> <br />|Result <br /> <br />|
|--------------|----------|
|Sqrt(*Input1*) <br /> <br />|**0** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />|
|Sqrt(*Input2*) <br /> <br />|**8.882567196480981** <br /> <br />|
|Sqrt(*Input3*, 5) <br /> <br />|**NaN** <br /> <br />*Input3* is NaN (Not a Number) because the input is negative. <br /> <br />|
|Sqrt(*Input1*)+Sqrt(*Input2*)&#42;Sqrt(*Input3*) <br /> <br />|0 + 8.882567196480981 &#42; NaN = **NaN** <br /> <br />*Input1* is 0 because the conversion to a double fails. <br /> <br />*Input3* is NaN because the string is a negative number. <br /> <br />Any arithmetic operation that involves NaN will result in NaN. <br /> <br />|
|Sqrt(*Input2*)+Round(*Input3*, 1)&#42;Abs(*Input1*) <br /> <br />|8.882567196480981 + (-123.1) &#42; 0 = <br /> <br />8.882567196480981 + (-123.1) = **-114.217432803519** <br /> <br />Input1 is 0 because the conversion to a double fails. <br /> <br />(-123.1 &#42; 0): Remember with multiplication, if only one of the arguments can be successfully converted to double, then the value of that argument is returned. <br /> <br />|

## Error and Data Handling
If an error occurs with an **Arithmetic Expression**[!INCLUDE[mapop](/Token/mapop_md.md)], by default, the entire [!INCLUDE[transform](/Token/transform_md.md)] is aborted. This error handling behavior is configurable. See **Error and Data Handling** at [Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md).

## See Also
[Logical Expression Examples: BizTalk Services](/Topic/Logical_Expression_Examples__BizTalk_Services.md)
[If-Then-Else Expression Example: BizTalk Services](/Topic/If-Then-Else_Expression_Example__BizTalk_Services.md)
[Conditional Assignment Example: BizTalk Services](/Topic/Conditional_Assignment_Example__BizTalk_Services.md)
[Expressions in BizTalk Services - Usage and Examples](/Topic/Expressions_in_BizTalk_Services_-_Usage_and_Examples.md)

