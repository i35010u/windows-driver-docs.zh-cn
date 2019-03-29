---
title: MASM 表达式与C++ 表达式
description: MASM 表达式与
ms.assetid: 3ec06b61-9f17-49b1-b7c5-66a349b5d275
keywords:
- 表达式中，MASM 和 c + +
- MASM 表达式，MASM vs。C++
- C + + 表达式，c + + vs。MASM
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1d4670e112e5b0c33ddcc1bb95d41093d7fe96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575232"
---
# <a name="masm-expressions-vs-c-expressions"></a>MASM 表达式与C++ 表达式


## <span id="ddk_masm_expressions_vs__c_expressions_dbg"></span><span id="DDK_MASM_EXPRESSIONS_VS__C_EXPRESSIONS_DBG"></span>


MASM 表达式计算和 c + + 表达式计算的最重要区别是，如下所示：

-   在 MASM 表达式中，任何符号的数字值是其内存地址。 在 c + + 表达式中，变量的数值为其实际值，而不是其地址。 数据结构不具有数字值。 相反，它们被视为实际的结构和必须相应地使用它们。 函数名或任何其他入口点的值是内存地址，并将被视为函数指针。 如果使用与 c + + 数据类型 （例如未修改的模块名称） 不对应的符号，将发生语法错误。

-   MASM 表达式计算器将视为 ULONG64 值的所有数字。 C + + 表达式计算器将强制转换到 ULONG64 的数字，并会保留所有数据类型的类型信息。

-   MASM 表达式计算器，您可以使用任何运算符和任意数量。 如果使用运算符和不正确的数据类型，c + + 表达式计算器将生成错误。

-   MASM 表达式计算器中, 按原义执行所有运算。 在 c + + 表达式计算器，指针算法正确缩放，并不合适时不允许使用。

-   MASM 表达式可以使用两个下划线 ( **\_ \_** ) 或两个冒号 ( **::** ) 以指示类的成员。 C + + 表达式计算器使用仅两个冒号语法。 调试器*输出*始终使用两个冒号。

-   在 MASM 表达式中，应将添加 at 符号 (**@**) 之前的最常见的寄存器除外。 如果省略此 at 符号，作为一个十六进制数字或符号可能会解释寄存器名。 在 c + + 表达式中，此前缀是必需的所有寄存器。

-   MASM 表达式可能包含对源行的引用。 这些引用所指示的抑音符 ( **\`** )。 不能引用在 c + + 表达式中的源行号。

 

 





