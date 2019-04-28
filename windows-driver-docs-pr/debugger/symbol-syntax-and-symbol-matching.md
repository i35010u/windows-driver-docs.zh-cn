---
title: 符号语法和符号匹配
description: 符号语法和符号匹配
ms.assetid: 7fda24bf-57be-4c7d-9eff-bd688de7cf1b
keywords:
- 符号，符号语法
- 符号，符号匹配
- 符号，符号后缀
- $ （本地符号标识符） 的命令的语法规则
- $ （本地符号标识符）
- 本地符号标识符 （$）
- 本地变量，本地符号标识符 （$）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07451ed31f6d92f26ebbadfbddadd9ca6bf6f932
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335499"
---
# <a name="symbol-syntax-and-symbol-matching"></a>符号语法和符号匹配


## <span id="ddk_symbol_syntax_and_symbol_matching_dbg"></span><span id="DDK_SYMBOL_SYNTAX_AND_SYMBOL_MATCHING_DBG"></span>


符号，可以直接在处理由正在调试的程序的令牌。 例如，可以在函数处设置断点**主要**使用命令**bp 主要**，或显示整数变量**MyInt**使用命令**ddMyInt L1**。

在许多情况下，符号可以用作调试器命令中的参数。 支持此操作对于大多数的数值参数，从而也支持某些文本参数中。 除了用于符号语法的一般规则，也有符号语法规则中的这种情况下每个应用中。

### <a name="span-idgeneralsymbolsyntaxrulesspanspan-idgeneralsymbolsyntaxrulesspangeneral-symbol-syntax-rules"></a><span id="general_symbol_syntax_rules"></span><span id="GENERAL_SYMBOL_SYNTAX_RULES"></span>常规符号语法规则

符号名称包含的一个或多个字符，但最初以字母、 下划线 (**\_**)、 问号 (**？**)，或美元符号 (**$**).

可能由模块名称限定的符号名称。 一个感叹号 (**！**) 将模块名称与符号分隔开来 (例如， **mymodule ！ 主要**)。 如果使用没有模块名称，则该符号仍前缀可以是一个感叹号。 使用一个感叹号没有模块名称可能非常有用，即使对于本地变量，以指示参数是一个名称并不是十六进制数字的调试器命令。 例如，变量**淡**将通过读取[ **dt （显示类型）** ](dt--display-type-.md)命令作为一个地址，除非其前缀为感叹号，或使用-n 选项。 但是，若要指定一个符号是本地的前面加上美元符号 （$） 和感叹号 （！ )，如 **$！ 酸橙色**。

符号名称是完全不区分大小写。 这意味着，是否存在**myInt**和一个**MyInt**中通过调试程序，程序将无法正确了解; 引用了一个其中任何命令可以访问，另一个，而不考虑如何该命令采用大写形式。

### <a name="span-idsymbolsyntaxinnumericalexpressionsspanspan-idsymbolsyntaxinnumericalexpressionsspansymbol-syntax-in-numerical-expressions"></a><span id="symbol_syntax_in_numerical_expressions"></span><span id="SYMBOL_SYNTAX_IN_NUMERICAL_EXPRESSIONS"></span>数值表达式中的符号语法

调试器无法识别两个不同类型的表达式：Microsoft Macro Assembler (MASM) 表达式和C++表达式。 符号是而言，这两种形式的语法不同，如下所示：

-   在 MASM 表达式中，每个符号被解释为一个地址。 具体取决于符号所引用的内容，这将是全局变量、 本地变量、 函数、 段、 模块或任何其他可识别的标签的地址。

-   在C++表达式，每个符号解释根据其类型。 具体取决于符号所引用的内容，可能被解释为整数、 数据结构、 函数指针或任何其他数据类型。 不对应的符号C++数据类型 （例如未修改的模块名称） 将导致语法错误。

有关何时以及如何使用每种类型的语法的说明，请参阅[评估表达式](evaluating-expressions.md)。

如果使用 MASM 表达式语法中，任何无法解释为十六进制数字还是寄存器的符号 (例如， **BadFeed**， **ebX**) 应始终为前缀为感叹号。 这可确保调试程序将其识别为一个符号。

[ **Ss （设置符号后缀）** ](ss--set-symbol-suffix-.md)命令可用于设置符号后缀。 这会指示调试器自动将"A"或"W"追加到否则找不到任何符号名称。

ASCII 和 Unicode 版本中存在许多 Win32 例程。 这些例程通常有一个"A"或"W"分别追加到其名称的末尾。 这些符号搜索时，使用符号后缀将提供协助调试程序。

后缀匹配不处于活动状态，默认值。

### <a name="span-idsymbolsyntaxintextexpressionsspanspan-idsymbolsyntaxintextexpressionsspansymbol-syntax-in-text-expressions"></a><span id="symbol_syntax_in_text_expressions"></span><span id="SYMBOL_SYNTAX_IN_TEXT_EXPRESSIONS"></span>文本表达式中的符号语法

符号可以使用中的文本参数的一些命令-例如， [ **bm （设置断点）** ](bp--bu--bm--set-breakpoint-.md)并[ **x （检查符号）**](x--examine-symbols-.md)。

这些文本参数支持通配符和说明符不同。 请参阅[字符串通配符语法](string-wildcard-syntax.md)有关详细信息。 除了标准字符串通配符前缀用来指定符号的文本表达式可以是前导下划线。 在匹配这对符号时，调试器会将此视为任意数量的下划线，甚至零。

文本表达式中匹配的符号时，不使用符号后缀。

 

 





