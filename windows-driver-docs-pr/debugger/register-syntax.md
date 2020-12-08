---
title: 寄存器语法
description: 寄存器语法
keywords:
- 表达式，寄存器
- 寄存器，命令语法
- " (注册前缀) "
- '命令的语法规则， (寄存器前缀) '
- 命令的语法规则，寄存器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7649cc4b8a17952a4575e44ebc64fd90ab13e2dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825775"
---
# <a name="register-syntax"></a>寄存器语法


## <span id="ddk_register_syntax_dbg"></span><span id="DDK_REGISTER_SYNTAX_DBG"></span>


调试器可以控制寄存器和浮点寄存器。

在表达式中使用寄存器时，应在寄存器前添加一个 at 符号 ( **@** ) 。 此 at 符号通知调试器以下文本是寄存器的名称。

如果使用的是 MASM 表达式语法，则可以省略某些非常常见寄存器的 at 符号。 在基于 x86 的系统上，可以省略 **eax**、 **ebx**、 **ecx**、 **edx**、 **esi**、 **edi**、 **ebp**、 **eip** 和 **efl** 寄存器的 at 符号。 但是，如果指定不带 at 符号的不太常见寄存器，调试器将首先尝试将文本解释为十六进制数。 如果文本包含非十六进制字符，则调试器会将文本解释为符号。 最后，如果调试器没有找到符号匹配项，则调试器会将文本解释为寄存器。

如果使用 c + + 表达式语法，则始终需要 at 符号。

[**R (寄存器)**](r--registers-.md)命令是此规则的例外情况。 调试器始终将其第一个参数解释为寄存器。  (at 符号不是必需的或不允许的。 ) 如果 **r** 命令有另一个参数，则将根据默认表达式语法对其进行解释。 如果默认表达式语法是 c + +，则必须使用以下命令将 **ebx** 注册复制到 **eax** 寄存器。

```dbgcmd
0:000> r eax = @ebx
```

有关特定于每个处理器的寄存器和说明的详细信息，请参阅 [处理器体系结构](processor-architecture.md)。

### <a name="span-idflags_on_an_x86_based_processorspanspan-idflags_on_an_x86_based_processorspanflags-on-an-x86-based-processor"></a><span id="flags_on_an_x86_based_processor"></span><span id="FLAGS_ON_AN_X86_BASED_PROCESSOR"></span>基于 x86 的处理器上的标志

基于 x86 的处理器也使用几个称为 *标志* 的1位寄存器。 有关这些标志的详细信息以及可用于查看或更改它们的语法，请参阅 [X86 标志](x86-architecture.md#x86-flags)。

### <a name="span-idregisters_and_threadsspanspan-idregisters_and_threadsspanregisters-and-threads"></a><span id="registers_and_threads"></span><span id="REGISTERS_AND_THREADS"></span>注册和线程

每个线程都有自己的寄存器值。 当线程正在执行时，这些值存储在 CPU 寄存器中，另一个线程在执行时存储在内存中。

在用户模式下，对寄存器的任何引用都会被解释为与当前线程关联的寄存器。 有关当前线程的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下，对寄存器的任何引用都会被解释为与当前注册上下文关联的寄存器。 您可以将注册上下文设置为与特定线程、上下文记录或捕获帧匹配。 对于指定的寄存器上下文，只能显示最重要的寄存器，并且无法更改其值。

 

 





