---
title: 计算表达式
description: 计算表达式
ms.assetid: f2fbdac1-2c20-4132-b43e-4c7a90a2f5b7
keywords:
- 表达式概述
- 不同类型的表达式
- MASM 表达式，何时使用
- C++表达式，何时使用
- MASM 表达式概述
- C++表达式概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 107b2371f223bb31933bfcfc346496fcfd8d4820
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379444"
---
# <a name="evaluating-expressions"></a>计算表达式


## <span id="ddk_evaluating_expressions_dbg"></span><span id="DDK_EVALUATING_EXPRESSIONS_DBG"></span>


调试器无法识别两种不同形式的表达式：*MASM 表达式*并*C++表达式*。

Microsoft Macro Assembler (MASM) 时使用表达式的示例中此帮助文档，除外另有说明。 MASM 表达式中的所有符号被都视为地址。

C++表达式是在实际中使用的相同C++代码。 在这些表达式中，符号被理解为适当的数据类型。

### <a name="span-idwheneachsyntaxisusedspanspan-idwheneachsyntaxisusedspanwhen-each-syntax-is-used"></a><span id="when_each_syntax_is_used"></span><span id="WHEN_EACH_SYNTAX_IS_USED"></span>当使用每个语法

可以选择默认表达式计算器中的以下方法之一：

-   使用\_NT\_EXPR\_EVAL[环境变量](general-environment-variables.md)启动调试器之前。

-   使用 **-ee** {**masm**|**c + +**}[命令行选项](command-line-options.md)启动调试器时。

-   使用[ **.expr （选择表达式计算器）** ](-expr--choose-expression-evaluator-.md)命令来显示或更改后运行调试器表达式计算器。

如果不使用上述方法之一，调试器将使用 MASM 表达式计算器。

如果你想要计算的表达式，而无需更改调试器状态，则可以使用[ **？（计算表达式）** ](---evaluate-expression-.md)命令。

所有命令和信息的调试窗口都解释其参数通过默认表达式计算器，但存在以下例外：

-   [ **??(评估C++表达式)** ](----evaluate-c---expression-.md)命令始终使用C++表达式计算器。

-   始终使用监视窗口C++表达式计算器。

-   [局部变量窗口](locals-window.md)始终使用C++表达式计算器。

-   某些扩展命令始终使用 MASM 表达式计算器 （和其他扩展命令接受仅数字参数而不是完整的表达式）。

-   如果表达式的任意部分括在括号中，并且您插入两个 at 符号 (**@@**) 先于表达式，计算该表达式，通过将通常不会使用这种情况下，表达式计算器。

这两个 at 符号 (**@@**) 使你能够使用单个命令的不同参数的两个不同的评估器。 它还可以通过不同方法评估长表达式的不同部分。 您可以嵌套两个 at 符号。 这两个 at 符号的每个外观切换到其他表达式计算器。

**警告**   C++表达式语法可用于处理结构和变量，但并不很适合用于调试程序命令的参数的分析器。 当将实现常规目的使用调试器命令或使用调试器扩展时，您应该设置为默认表达式计算器的 MASM 表达式语法。 如果您必须拥有特定的参数使用C++表达式语法中，使用这两个 at 符号 (**@@**) 语法。

 

有关两种不同的表达式类型的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

### <a name="span-idnumbersinexpressionsspanspan-idnumbersinexpressionsspannumbers-in-expressions"></a><span id="numbers_in_expressions"></span><span id="NUMBERS_IN_EXPRESSIONS"></span>在表达式中的数字

根据当前的基数进行解释的 MASM 表达式中的数字。 [ **N (设置数量 Base)** ](n--set-number-base-.md)命令可用于设置默认基数为 16、 10 或 8。 不带前缀的所有数字将被都解释此库中。 可以通过指定重写默认基数**0x**前缀 （十六进制） **0n**前缀 （十进制） **0t**前缀 （八进制） 或**0y**前缀 （二进制）。

统计中的C++除非以不同的方式指定，否则，表达式被解释为十进制数字。 若要指定十六进制整数，添加**0x**数字前。 若要指定八进制整数，添加**0**数之前 （零）。 (但是，在调试器的*输出*，则**0n**有时使用十进制的前缀。)

如果你想要在同一时间在几个基本中显示一个数字，使用[ **（显示数字格式） 的.formats** ](-formats--show-number-formats-.md)命令。

### <a name="span-idsymbolsinexpressionsspanspan-idsymbolsinexpressionsspansymbols-in-expressions"></a><span id="symbols_in_expressions"></span><span id="SYMBOLS_IN_EXPRESSIONS"></span>表达式中的符号

两种类型的表达式以不同的方式解释的符号：

-   在 MASM 表达式中，每个符号被解释为一个地址。 具体取决于符号所引用的内容，此地址是全局变量、 本地变量、 函数、 段、 模块或任何其他可识别的标签的地址。

-   在C++表达式，每个符号解释根据其类型。 具体取决于符号所引用的内容，可能会被解释为整数、 数据结构、 函数指针或任何其他数据类型。 不对应的符号C++数据类型 （例如未修改的模块名称），则创建一个语法错误。

如果符号可能不明确，加上的模块名称和一个感叹号 ( **！** )。 如果符号名无法解释为十六进制数，加上的模块名称和一个感叹号 ( **！** ) 或仅一个感叹号。 若要指定符号要作为本地，省略模块名称，并包括美元符号和感叹号 ( **$！** ) 的符号名称前。 有关解释符号的详细信息，请参阅[符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

### <a name="span-idoperatorsinexpressionsspanspan-idoperatorsinexpressionsspanoperators-in-expressions"></a><span id="operators_in_expressions"></span><span id="OPERATORS_IN_EXPRESSIONS"></span>表达式中的运算符

每个表达式类型使用的运算符不同的集合。

有关可以在的 MASM 表达式和其优先顺序规则中使用的运算符的详细信息，请参阅[MASM 数字和运算符](masm-numbers-and-operators.md)。

有关可以在中使用的运算符详细信息C++表达式和其优先顺序规则，请参阅[C++数字和运算符](c---numbers-and-operators.md)。

请记住，MASM 操作始终基于字节和C++操作遵循C++类型 （包括指针算法的缩放） 的规则。

有关不同的语法的一些示例，请参阅[表达式示例](expression-examples.md)。

 

 





