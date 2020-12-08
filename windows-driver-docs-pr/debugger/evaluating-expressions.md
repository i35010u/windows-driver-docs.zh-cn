---
title: 计算表达式
description: 计算表达式
keywords:
- 表达式，概述
- 表达式，不同类型
- MASM 表达式，何时使用
- C + + 表达式，何时使用
- MASM 表达式，概述
- C + + 表达式，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3213ece6ebc8037cdc244e98449c93b1267b04c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831951"
---
# <a name="evaluating-expressions"></a>计算表达式


## <span id="ddk_evaluating_expressions_dbg"></span><span id="DDK_EVALUATING_EXPRESSIONS_DBG"></span>


调试器理解两种不同形式的表达式： *MASM 表达式* 和 *c + + 表达式*。

此帮助文档的示例中使用了 Microsoft 宏组装器 (MASM) 表达式，除非另有说明。 在 MASM 表达式中，所有符号被视为地址。

C + + 表达式与实际 c + + 代码中使用的表达式相同。 在这些表达式中，符号被理解为适当的数据类型。

### <a name="span-idwhen_each_syntax_is_usedspanspan-idwhen_each_syntax_is_usedspanwhen-each-syntax-is-used"></a><span id="when_each_syntax_is_used"></span><span id="WHEN_EACH_SYNTAX_IS_USED"></span>当使用每个语法时

可以通过以下方法之一选择默认表达式计算器：

-   在 \_ 启动调试器之前，请使用 NT \_ EXPR \_ EVAL [环境变量](general-environment-variables.md) 。

-   启动调试器时，使用 **-ee** {**masm** | **c + +**}[命令行选项](command-line-options.md)。

-   使用 [**expr (选择表达式计算器)**](-expr--choose-expression-evaluator-.md) 命令在调试器运行后显示或更改表达式计算器。

如果不使用上述方法之一，则调试器将使用 MASM 表达式计算器。

如果您想要在不更改调试器状态的情况下计算表达式，则可以使用 [**？ (计算 expression)**](---evaluate-expression-.md) 命令。

所有命令和调试信息 windows 都通过默认表达式计算器来解释它们的参数，但以下情况例外：

-   " [**(" 计算 c + + 表达式)**](----evaluate-c---expression-.md) 命令始终使用 c + + 表达式计算器。

-   监视窗口始终使用 c + + 表达式计算器。

-   " [局部变量" 窗口](locals-window.md) 始终使用 c + + 表达式计算器。

-   某些扩展命令始终使用 MASM 表达式计算器 (并且其他扩展命令仅接受数值参数，而不接受) 的完整表达式。

-   如果表达式的任何部分都括在括号内，并且你在表达式之前插入两个 at 符号 (**@@**) ，则表达式计算器将计算该表达式，该表达式计算器通常不会用于此情况。

这两个 at 符号 (**@@**) 使你可以对单个命令的不同参数使用两个不同的计算器。 它还使您可以通过不同的方法来评估长表达式的不同部分。 可以嵌套两个 at 符号。 两个 at 符号的每个外观都切换到另一个表达式计算器。

**警告**   C + + 表达式语法对处理结构和变量非常有用，但它并不适合用作调试器命令的参数的分析器。 如果出于一般目的使用调试程序命令，或者使用调试器扩展，则应将 MASM 表达式语法设置为默认表达式计算器。 如果必须使用 c + + 表达式语法的特定参数，请使用两个 at 符号 (**@@**) 语法。

 

有关这两种不同表达式类型的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

### <a name="span-idnumbers_in_expressionsspanspan-idnumbers_in_expressionsspannumbers-in-expressions"></a><span id="numbers_in_expressions"></span><span id="NUMBERS_IN_EXPRESSIONS"></span>表达式中的数字

MASM 表达式中的数字根据当前基数来解释。 [**N (Set Number Base)**](n--set-number-base-.md)命令可用于将默认基数设置为16、10或8。 将在此基准中解释所有未加前缀的数字。 可以通过指定 **0x** 前缀 (十六进制) 、 **0n** 前缀 (decimal) 、 **0t** 前缀 (八进制) 或 **w..1 ....** 前缀 (binary) 来替代默认基数。

C + + 表达式中的数字被解释为十进制数，除非指定了不同的值。 若要指定十六进制整数，请在数字前面加上 **0x** 。 若要指定八进制整数，请在数字前面加上 **0** (零) 。  (但是，在调试器的 *输出* 中，有时会使用 **0n** 小数前缀。 ) 

如果要同时在多个基中显示数字，请使用 [**. formats (在) 命令中显示数字格式**](-formats--show-number-formats-.md) 。

### <a name="span-idsymbols_in_expressionsspanspan-idsymbols_in_expressionsspansymbols-in-expressions"></a><span id="symbols_in_expressions"></span><span id="SYMBOLS_IN_EXPRESSIONS"></span>表达式中的符号

两种类型的表达式以不同的方式解释符号：

-   在 MASM 表达式中，每个符号被解释为一个地址。 根据符号引用的内容，此地址是全局变量、局部变量、函数、段、模块或任何其他可识别标签的地址。

-   在 c + + 表达式中，将根据符号的类型解释每个符号。 根据符号的引用，可能会将其解释为整数、数据结构、函数指针或任何其他数据类型。 不对应于 c + + 数据类型的符号 (如未修改的模块名称) 创建语法错误。

如果符号可能不明确，请在其前面加上模块名称，将感叹号 ( **！** ). 如果符号名称可以解释为十六进制数，请在其前面加上模块名称，将感叹号 ( **！** ) 或仅惊叹号。 若要指定某个符号应为本地符号，请省略该模块名称，并将一个货币符号和一个惊叹号 ( **$！** 符号名称前 ) 。 有关解释符号的详细信息，请参阅 [符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

### <a name="span-idoperators_in_expressionsspanspan-idoperators_in_expressionsspanoperators-in-expressions"></a><span id="operators_in_expressions"></span><span id="OPERATORS_IN_EXPRESSIONS"></span>表达式中的运算符

每个表达式类型使用不同的运算符集合。

若要详细了解可以在 MASM 表达式及其优先规则中使用的运算符，请参阅 [Masm 数字和运算符](masm-numbers-and-operators.md)。

有关可在 c + + 表达式及其优先规则中使用的运算符的详细信息，请参阅 [c + + 编号和运算符](c---numbers-and-operators.md)。

请记住，MASM 操作始终基于字节，而 c + + 操作遵循 c + + 类型规则 (包括指针算法) 的缩放。

有关不同语法的一些示例，请参阅 [表达式示例](expression-examples.md)。

 

 





