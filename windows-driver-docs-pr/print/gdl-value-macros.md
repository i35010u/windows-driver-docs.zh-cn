---
title: GDL 值宏
description: GDL 值宏
keywords:
- GDL WDK，宏
- 宏 WDK GDL，值宏
- 值宏 WDK GDL
- 值 WDK GDL，值宏
- 宏指令 WDK GDL
- 宏 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a80f354a3cf2268de19941c29395626d6ac3e591
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835885"
---
# <a name="gdl-value-macros"></a>GDL 值宏


*值宏* 用于表示值的全部或部分。 它们是在宏构造中定义的 \* 。 可以在一个构造中定义多个宏。

宏构造中的每个项 \* 都是一个单独的宏。 项的关键字成为值宏的名称，该项的值将成为该值宏的内容。 宏名必须是符号名称类型。 值宏的内容可以是符合有效的 GDL 语法的任何值。

值宏可以引用其他值宏。 宏构造的实例名称 \* 可以包含后面跟有括号括起来的形参表的标记。 宏构造中任何宏定义的任何形参引用 \* 均被符号替换为实际引用值宏时传入的相应参数。

**注意**  将用于传递值宏引用的参数的声明和引用以等号 (=) 为前缀，表示该参数类型为值宏。
对值宏的所有引用还带有等号 (=) ，以表示引用是值宏而不是块宏。 等号后面必须紧跟值宏名称，并且不允许使用中间空格。 对值宏的引用可以将参数列表嵌套到任意深度。

 

### <a name="macro-examples"></a><a href="" id="macro-examples"></a> 宏示例

所有值宏定义都必须被识别为完整的有效值实体。

下面的代码示例演示如何使用值宏。

```cpp
*Macros:
{
    InvalidMacro: "First Half of a string
}
```

InvalidMacro 无效，因为带引号的字符串上下文必须以双引号结束。 此未终止的字符串不是完整值。

如果要表示不完整的值实体，请使用下面的代码示例。

```cpp
*Macros:
{
    FirstHalf: <BeginValue:Q>"This is the first half <EndValue:Q>
    SecondHalf:  <BeginValue:Q>of the string."<EndValue:Q>
}
*FullString: =FirstHalf=SecondHalf
*%  *FullString now expands to generate the complete string:
*FullString: "This is the first half of the string."
```

下面的代码演示如何使用宏参数。

```cpp
*Macros: FormalArgs(=arg1, =arg2)
{
result1: disappointed
result2: pleased
result3: impressed
result4: awestruck
result5: restrained


adverb1: very =arg1 and =arg2
   adverb2: while remaining =arg1
   String1:  The audience was =arg1 with today's performance.
}
```

下面的代码演示如何将宏引用与参数一起使用。

```cpp
*BadOutput: =String1(=result1)
*GoodOutput: =String1(=adverb1(=adverb1(=result2, =result3), =adverb2(=result5)))
```

分析器将展开前面的宏引用以生成以下代码。

```cpp
*BadOutput: The audience was disappointed with today's performance.
*GoodOutput: The audience was very very pleased and impressed and while remaining restrained with today's performance.
```

在所有值上下文中都不能识别值宏引用。 例如，不能在任意值或带引号的字符串上下文内识别值宏。 但在可能驻留在带引号的字符串上下文内的十六进制字符串上下文内可识别值宏。

为了提供与 GPD 的向后兼容性，百分号 (% ) 被解释为表示当在值宏定义的内容内的非文本空白值上下文中使用百分号时，它会引入一个命令参数上下文。 换句话说，除非定义了命令参数，或者在文本空白上下文中包含百分号，如 Begin/EndValue，否则应避免在值宏定义内使用百分号 &lt; &gt; 。

仅当在任何宏定义之外引用宏时，才会实际解释宏定义的内容。 此时，被引用的宏会替换为其内容，并且实际会解释内容。 如果内容包含宏引用，该引用将替换为其内容，并且会继续解释该宏的内容。

应将分析器视为对单个输入流进行操作。 如果在任何宏定义以外检测到宏引用，则会从输入流中删除宏引用并将其替换为其内容，并使用宏的内容继续分析输入流。

请看下面的宏。

```cpp
*Macros:
{
quote: <BeginValue:x>"<EndValue:x>
first_half: =quote This is enclosed
second_half:  by quotes.=quote
whole_string: =first_half <not a hex string!> =second_half
}
*Print1: =quote
*Print2: =first_half
*Print3: =second_half
*Print4: =whole_string
```

上述宏将扩展到以下代码。

```cpp
*Print1:  "
*Print2:  " This is enclosed
*Print3:  by quotes."
*Print4:  " This is enclosed <not a hex string!> by quotes."
```

请注意，展开的结果不是语法上合法的 GDL。

 

 




