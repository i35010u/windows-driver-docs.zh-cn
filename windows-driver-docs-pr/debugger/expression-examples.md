---
title: 表达式示例
description: 表达式示例
keywords:
- 表达式，示例
- MASM 表达式，示例
- C + + 表达式，示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d948792460df2a3480aaee6e0fb97bba45dea712
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838215"
---
# <a name="expression-examples"></a>表达式示例


## <span id="ddk_expression_examples_dbg"></span><span id="DDK_EXPRESSION_EXAMPLES_DBG"></span>


本主题包含各种命令中使用的 MASM 和 c + + 表达式的示例。

本帮助文档的所有其他部分都将使用示例中的 MASM 表达式语法，除非另有说明)  (。 C + + 表达式语法对处理结构和变量非常有用，但它不会很好地分析调试器命令的参数。

如果使用调试程序命令进行常规用途或使用调试器扩展，则应将 MASM 表达式语法设置为默认语法。 如果必须具有特定参数才能使用 c + + 表达式语法，请使用 **@ @ ( )** 语法。

### <a name="span-idconditional_breakpointsspanspan-idconditional_breakpointsspanconditional-breakpoints"></a><span id="conditional_breakpoints"></span><span id="CONDITIONAL_BREAKPOINTS"></span>条件断点

您可以使用比较运算符创建 [条件断点](setting-a-conditional-breakpoint.md)。 下面的代码示例使用了 MASM 表达式语法。 由于当前的默认基数为16，因此该示例使用 **0n** 前缀，以便将数字20理解为十进制数字。

```dbgcmd
0:000> bp MyFunction+0x43 "j ( poi(MyVar)>0n20 ) ''; 'gc' " 
```

在上面的示例中， **MyVar** 是 C 源中的一个整数。 由于 MASM 分析器将所有符号视为地址，因此该示例必须具有 **poi** 运算符才能取消引用 **MyVar**。

### <a name="span-idconditional_expressionsspanspan-idconditional_expressionsspanconditional-expressions"></a><span id="conditional_expressions"></span><span id="CONDITIONAL_EXPRESSIONS"></span>条件表达式

**如果 eax** 大于 **ebx**，则以下示例打印 **ecx** 的值，如果 eax 小于 ebx **，则打印** 3 **ebx**; 如果 **eax** 等于 **ebx**，则打印3。 此示例使用 MASM 表达式计算器，因此等号 (=) 是比较运算符，而不是赋值运算符。

```dbgcmd
0:000> ? ecx*(eax>ebx) + 7*(eax<ebx) + 3*(eax=ebx) 
```

在 c + + 语法中， **@** 符号表示寄存器，双等号 (= =) 是比较运算符，并且代码必须从 BOOL 显式转换为 **int**。因此，在 c + + 语法中，上一个命令将成为以下命令。

```dbgcmd
0:000> ?? @ecx*(int)(@eax>@ebx) + 7*(int)(@eax<@ebx) + 3*(int)(@eax==@ebx) 
```

### <a name="span-idc___expression_examplesspanspan-idc___expression_examplesspanc-expression-examples"></a><span id="c___expression_examples"></span><span id="C___EXPRESSION_EXAMPLES"></span>C + + 表达式示例

如果 **myInt** 是一个 ULONG32 值，并且使用的是 MASM 表达式计算器，则以下两个示例显示了 **myInt** 的值。

```dbgcmd
0:000> ?? myInt 
0:000> dd myInt L1 
```

但是，以下示例显示了 **myInt** 的 *地址*。

```dbgcmd
0:000> ? myInt 
```

### <a name="span-idmixed_expression_examplesspanspan-idmixed_expression_examplesspanmixed-expression-examples"></a><span id="mixed_expression_examples"></span><span id="MIXED_EXPRESSION_EXAMPLES"></span>混合表达式示例

在 c + + 表达式中不能使用源行表达式。 下面的示例使用 **@ @ ( )** 语法在 c + + 表达式中嵌套 MASM 表达式。 此示例将 **MyPtr** 设置为 myfile.txt 文件的第43行的地址。

```dbgcmd
0:000> ?? MyPtr = @@( `myfile.c:43` )
```

下面的示例将默认表达式计算器设置为 MASM，然后将 *表达式值计算为* c + + 表达式，并将 *表达式* 2 和 *Expression3* 作为 MASM 表达式进行计算。

```dbgcmd
0:000> .expr /s masm 
0:000> bp Expression1 + @@( Expression2 ) + Expression3 
```

如果 **myInt** 是 ULONG64 值，并且你知道此值在内存中由另一个 ULONG64 后跟，则可以使用以下示例之一在该位置设置访问断点。  (注意指针算法的使用。 ) 

```dbgcmd
0:000> ba r8 @@( &myInt + 1 ) 
0:000> ba r8 myInt + 8 
```

### <a name="span-idstructuresspanspan-idstructuresspanstructures"></a><span id="structures"></span><span id="STRUCTURES"></span>构造

C + + 表达式计算器将伪寄存器强制转换为相应的类型。 例如， **$teb** 将强制转换为 teb \* 。 下面的示例显示了进程 ID。

```dbgcmd
kd> ??  @$teb->ClientId.UniqueProcess 
```

 

 





