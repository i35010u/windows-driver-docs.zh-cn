---
title: 表达式示例
description: 表达式示例
ms.assetid: a4915678-a83f-48f1-8b29-50cf530f9246
keywords:
- 表达式示例
- MASM 表达式示例
- C++表达式示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed6c9a91302443231dfda10146aee8c4e9fba2f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379743"
---
# <a name="expression-examples"></a>表达式示例


## <span id="ddk_expression_examples_dbg"></span><span id="DDK_EXPRESSION_EXAMPLES_DBG"></span>


本主题包含示例的 MASM 和C++的各种命令中使用的表达式。

此帮助文档的所有其他部分使用 MASM 表达式语法示例中，（除非另有说明）。 C++表达式语法用于处理结构和变量，非常有用，但它并不很好地分析调试器命令的参数。

如果要实现常规目的使用调试器命令，或使用调试器扩展，您应该设置为默认语法的 MASM 表达式语法。 如果您必须拥有特定的参数，以使用C++表达式语法中，使用 **@ @ （)** 语法。

### <a name="span-idconditionalbreakpointsspanspan-idconditionalbreakpointsspanconditional-breakpoints"></a><span id="conditional_breakpoints"></span><span id="CONDITIONAL_BREAKPOINTS"></span>条件断点

可以使用比较运算符来创建[条件断点](setting-a-conditional-breakpoint.md)。 下面的代码示例使用 MASM 表达式语法。 因为当前的默认基数为 16，该示例使用**0n**前缀，以便数字 20 理解为十进制数。

```dbgcmd
0:000> bp MyFunction+0x43 "j ( poi(MyVar)>0n20 ) ''; 'gc' " 
```

在上一示例中， **MyVar**是 C 源中的一个整数。 示例由于 MASM 分析器将作为地址的所有符号，必须具有**poi**运算符来取消**MyVar**。

### <a name="span-idconditionalexpressionsspanspan-idconditionalexpressionsspanconditional-expressions"></a><span id="conditional_expressions"></span><span id="CONDITIONAL_EXPRESSIONS"></span>条件表达式

下面的示例将的值打印**ecx**如果**eax**大于**ebx**7 中，如果**eax**是小于**ebx**，和 3 个 if **eax**等于**ebx**。 此示例使用 MASM 表达式计算器，所以等号 （=） 是一个比较运算符，不是赋值运算符。

```dbgcmd
0:000> ? ecx*(eax>ebx) + 7*(eax<ebx) + 3*(eax=ebx) 
```

在C++语法中， **@** 符号指示寄存器，双等号 （= =） 是比较运算符，代码必须显式强制转换为 bool **int**。因此，在C++语法前, 一个命令将成为以下。

```dbgcmd
0:000> ?? @ecx*(int)(@eax>@ebx) + 7*(int)(@eax<@ebx) + 3*(int)(@eax==@ebx) 
```

### <a name="span-idcexpressionexamplesspanspan-idcexpressionexamplesspanc-expression-examples"></a><span id="c___expression_examples"></span><span id="C___EXPRESSION_EXAMPLES"></span>C++表达式示例

如果**myInt**是一个 ULONG32 值，如果使用的 MASM 表达式计算器，以下两个示例显示的值**MyInt**。

```dbgcmd
0:000> ?? myInt 
0:000> dd myInt L1 
```

但是，下面的示例演示*地址*的**myInt**。

```dbgcmd
0:000> ? myInt 
```

### <a name="span-idmixedexpressionexamplesspanspan-idmixedexpressionexamplesspanmixed-expression-examples"></a><span id="mixed_expression_examples"></span><span id="MIXED_EXPRESSION_EXAMPLES"></span>混合的表达式示例

不能使用源行中的表达式C++表达式。 下面的示例使用 **@ @ （)** 语法嵌套内的 MASM 表达式C++表达式。 此示例设置**MyPtr**等于 Myfile.c 文件的第 43 行的地址。

```dbgcmd
0:000> ?? MyPtr = @@( `myfile.c:43` )
```

下面的示例设置为 MASM 的默认表达式计算器，然后评估*Expression2*作为C++表达式，并评估*Expression1*并*Expression3*作为 MASM 表达式。

```dbgcmd
0:000> .expr /s masm 
0:000> bp Expression1 + @@( Expression2 ) + Expression3 
```

如果**myInt**是一个 ULONG64 值，如果您知道此值跟另一个 ULONG64 在内存中，您可以使用下面的示例之一，在该位置设置访问断点。 （请注意使用指针算法。）

```dbgcmd
0:000> ba r8 @@( &myInt + 1 ) 
0:000> ba r8 myInt + 8 
```

### <a name="span-idstructuresspanspan-idstructuresspanstructures"></a><span id="structures"></span><span id="STRUCTURES"></span>结构

C++表达式计算器将强制转换为相应类型的伪寄存器。 例如， **$teb**强制转换为 TEB\*。 下面的示例显示进程 id。

```dbgcmd
kd> ??  @$teb->ClientId.UniqueProcess 
```

 

 





