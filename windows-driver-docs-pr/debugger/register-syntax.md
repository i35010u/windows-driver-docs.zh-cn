---
title: 寄存器语法
description: 寄存器语法
ms.assetid: 64a566b1-c10b-4329-947c-af69904a21f8
keywords:
- 表达式寄存器
- 寄存器，命令语法
- （可在注册前缀）
- （注册前缀） 的命令的语法规则
- 语法规则的命令，注册
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79b4dfeea0548d23d0ca17bb31850bbf35a22478
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370205"
---
# <a name="register-syntax"></a>寄存器语法


## <span id="ddk_register_syntax_dbg"></span><span id="DDK_REGISTER_SYNTAX_DBG"></span>


调试器可以控制寄存器和浮点寄存器。

当在表达式中使用寄存器时，应添加 at 符号 ( **@** ) 之前注册。 在登录这将告知调试器以下文本是寄存器的名称。

如果使用 MASM 表达式语法，则可以省略某些非常常见的注册时注册。 在基于 x86 的系统中，则可以省略的符号开头**eax**， **ebx**， **ecx**， **edx**， **esi**， **edi**， **ebp**， **eip**，以及**推崇**注册。 但是，如果指定了不太常见的寄存器，而无需 at 符号，调试器首先尝试将解释为十六进制数字的文本。 如果文本包含非十六进制字符，在调试器下一步将文本解释为一个符号。 最后，如果调试器未找到符号匹配项，调试器会将文本解释为寄存器。

如果使用的C++表达式语法，at 符号始终是必需的。

[ **R （寄存器）** ](r--registers-.md)命令是此规则的例外。 调试器始终将其第一个参数解释为寄存器。 (在登录不要求或不允许。)如果没有为第二个参数**r**命令时，它根据默认表达式语法进行解释。 如果默认表达式语法是C++，必须使用以下命令将复制**ebx**注册到**eax**注册。

```dbgcmd
0:000> r eax = @ebx
```

有关寄存器和特定于每个处理器的说明的详细信息，请参阅[处理器体系结构](processor-architecture.md)。

### <a name="span-idflagsonanx86basedprocessorspanspan-idflagsonanx86basedprocessorspanflags-on-an-x86-based-processor"></a><span id="flags_on_an_x86_based_processor"></span><span id="FLAGS_ON_AN_X86_BASED_PROCESSOR"></span>在基于 x86 的处理器上的标志

基于 x86 的处理器还使用名为的几个 1 位寄存器*标志*。 有关这些标志和可用于查看或更改其语法的详细信息，请参阅[x86 标志](x86-architecture.md#x86-flags)。

### <a name="span-idregistersandthreadsspanspan-idregistersandthreadsspanregisters-and-threads"></a><span id="registers_and_threads"></span><span id="REGISTERS_AND_THREADS"></span>寄存器和线程

每个线程都具有其自己的注册值。 这些值存储在 CPU 寄存器时线程正在执行并在内存中执行另一个线程时。

在用户模式下，任何对寄存器的引用被解释为与当前线程相关联的寄存器。 有关当前线程的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

在内核模式下，任何对寄存器的引用被解释为与当前寄存器上下文关联的寄存器。 可以设置寄存器上下文以匹配特定线程、 上下文记录或捕获帧。 指定注册上下文，并且不能更改它们的值，可以显示仅最重要的注册。

 

 





