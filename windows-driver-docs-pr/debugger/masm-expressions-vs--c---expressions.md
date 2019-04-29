---
title: MASM 表达式与C++ 表达式
description: MASM 表达式与
ms.assetid: 3ec06b61-9f17-49b1-b7c5-66a349b5d275
keywords:
- 表达式中，MASM 和C++
- MASM 表达式，MASM vs。C++
- C++表达式中， C++ vs。MASM
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1d4670e112e5b0c33ddcc1bb95d41093d7fe96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383299"
---
# <a name="masm-expressions-vs-c-expressions"></a>MASM 表达式与C++ 表达式


## <span id="ddk_masm_expressions_vs__c_expressions_dbg"></span><span id="DDK_MASM_EXPRESSIONS_VS__C_EXPRESSIONS_DBG"></span>


MASM 表达式计算之间最大的区别和C++表达式计算如下所示：

-   在 MASM 表达式中，任何符号的数字值是其内存地址。 在C++表达式，变量的数值是实际值，不是其地址。 数据结构不具有数字值。 相反，它们被视为实际的结构和必须相应地使用它们。 函数名或任何其他入口点的值是内存地址，并将被视为函数指针。 如果使用不对应的符号C++数据类型 （如未修改的模块名称），会发生语法错误。

-   MASM 表达式计算器将视为 ULONG64 值的所有数字。 C++表达式计算器将强制转换到 ULONG64 数字和保留类型的所有数据类型的信息。

-   MASM 表达式计算器，您可以使用任何运算符和任意数量。 C++如果使用运算符和不正确的数据类型，表达式计算器将生成错误。

-   MASM 表达式计算器中, 按原义执行所有运算。 在C++表达式计算器正确缩放和不合适时不允许使用指针算法。

-   MASM 表达式可以使用两个下划线 ( **\_ \_** ) 或两个冒号 ( **::** ) 以指示类的成员。 C++表达式计算器使用仅两个冒号语法。 调试器*输出*始终使用两个冒号。

-   在 MASM 表达式中，应将添加 at 符号 (**@**) 之前的最常见的寄存器除外。 如果省略此 at 符号，作为一个十六进制数字或符号可能会解释寄存器名。 在C++表达式，该前缀是所必需的所有寄存器。

-   MASM 表达式可能包含对源行的引用。 这些引用所指示的抑音符 ( **\`** )。 不能引用中的源行号C++表达式。

 

 





