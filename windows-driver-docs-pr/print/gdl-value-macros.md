---
title: GDL 值宏
description: GDL 值宏
ms.assetid: 171245ef-d9ab-4c1d-86b9-f53ae10033b3
keywords:
- GDL WDK 宏
- 宏 WDK GDL，值宏
- 值宏 WDK GDL
- 值 WDK GDL，值宏
- 宏指令 WDK GDL
- 宏 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db551f8988ea4714ee24e524138b61173de1c82c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329872"
---
# <a name="gdl-value-macros"></a>GDL 值宏


*值宏*用来表示所有或值的一部分。 中定义\*宏构造。 您可以定义一个构造中的多个宏。

中的每个条目\*宏构造是单独的宏。 项的关键字将成为值宏的名称和条目的值将成为所指定值的宏的内容。 宏名称必须是符号名称类型。 值宏的内容可以是任何符合有效 GDL 语法，这些值。

值宏可以引用其他值宏。 实例名称\*宏构造可以容纳一个标记，后跟括号括起的形式自变量列表。 对任何宏定义中任何形式自变量的任何引用\*宏构造符号替换为实际引用值宏时传入的相应参数。

**请注意**  声明和引用将用于将值宏引用传递自变量的前缀为等号 （=） 来表示参数类型是值宏。
对值宏的所有引用以等号 （=） 以表示引用的是值宏而不是块宏还作为都前缀。 等号必须紧接着是按值宏名称，并允许任何干预空格。 对值宏的引用可以嵌套到任意深度的参数列表。

 

### <a href="" id="macro-examples"></a> 宏的示例

必须将所有值宏定义都识别为完整的有效值实体。

下面的代码示例演示如何使用值宏。

```cpp
*Macros:
{
    InvalidMacro: "First Half of a string
}
```

InvalidMacro 无效，因为必须以双引号结束带引号的字符串上下文。 此未终止的字符串不是完整值。

如果你想要表示不完整值实体，使用下面的代码示例。

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

下面的代码演示如何使用参数中使用宏的引用。

```cpp
*BadOutput: =String1(=result1)
*GoodOutput: =String1(=adverb1(=adverb1(=result2, =result3), =adverb2(=result5)))
```

分析器将扩展前面的宏引用，以生成下面的代码。

```cpp
*BadOutput: The audience was disappointed with today's performance.
*GoodOutput: The audience was very very pleased and impressed and while remaining restrained with today's performance.
```

在所有值上下文中无法识别宏值的引用。 例如，值宏不识别中的任意值或带引号的字符串的上下文。 但在可能位于带引号的字符串上下文中的十六进制字符串上下文中识别值宏。

若要提供向后的兼容性 GPD，百分号 （%）解释为表示百分比符号的值宏定义内容中的非文本空白值上下文中使用时，它引入命令参数上下文。 换而言之，应避免使用值宏定义中的百分号，除非要定义的命令参数或如文本空白上下文中包含百分号&lt;Begin/EndValue&gt;。

仅当在任何宏定义外部引用宏时，实际上解释宏定义的内容。 此时，其内容替换为引用的宏和实际解释内容。 如果内容包含宏引用，其内容替换为该引用并解释将继续使用该宏的内容。

应分析程序视为对单个输入流。 之外的任何宏定义检测到的宏引用时，从输入流中删除并由其内容替换为宏引用和分析的输入流将继续执行宏的内容。

请考虑下面的宏。

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

以前的宏将扩展到下面的代码。

```cpp
*Print1:  "
*Print2:  " This is enclosed
*Print3:  by quotes."
*Print4:  " This is enclosed <not a hex string!> by quotes."
```

请注意，扩展的结果不是语法上法律 GDL。

 

 




