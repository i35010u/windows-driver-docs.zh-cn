---
title: MASM 表达式与C++ 表达式
description: MASM 表达式与
keywords:
- 表达式、MASM 和 c + +
- MASM 表达式，MASM 与 c + +
- C + + 表达式，c + + 与 MASM
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0d5080633bbc3da8d5250939c6a3f268b653c91
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792401"
---
# <a name="masm-expressions-vs-c-expressions"></a>MASM 表达式与C++ 表达式


## <span id="ddk_masm_expressions_vs__c_expressions_dbg"></span><span id="DDK_MASM_EXPRESSIONS_VS__C_EXPRESSIONS_DBG"></span>


MASM 表达式计算与 c + + 表达式计算的最重要差异如下：

-   在 MASM 表达式中，任何符号的数字值都是它的内存地址。 在 c + + 表达式中，变量的数值是其实际值，而不是其地址。 数据结构没有数字值。 相反，它们被视为实际的结构，并且必须相应地使用它们。 函数名称或任何其他入口点的值为内存地址，并被视为函数指针。 如果使用与 c + + 数据类型不对应的符号 (如) 的未修改的模块名称，则会出现语法错误。

-   MASM 表达式计算器将所有数字视为 ULONG64 值。 C + + 表达式计算器将数字转换为 ULONG64，并保留所有数据类型的类型信息。

-   使用 MASM 表达式计算器可以将任何运算符与任意数字一起使用。 如果将运算符与错误的数据类型一起使用，c + + 表达式计算器会生成错误。

-   在 MASM 表达式计算器中，将按原义执行所有算术运算。 在 c + + 表达式计算器中，指针算法可正确缩放，在不适当的情况下不允许。

-   MASM 表达式可以使用两个下划线 ( **\_\_** ) 或两个冒号 ( **：：** ) 来指示类的成员。 C + + 表达式计算器仅使用双冒号语法。 调试器 *输出* 始终使用两个冒号。

-   在 MASM 表达式中，应在 **@** 除最常见寄存器之外的所有 () 添加 at 符号。 如果在符号处省略此符号，则寄存器名称可以解释为十六进制数或符号。 在 c + + 表达式中，所有寄存器都需要此前缀。

-   MASM 表达式可能包含对源行的引用。 这些引用由抑音符 ( ) 指示 **\`** 。 不能在 c + + 表达式中引用源行号。

 

 





