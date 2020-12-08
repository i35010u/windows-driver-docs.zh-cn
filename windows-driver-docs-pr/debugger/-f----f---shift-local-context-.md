---
title: .f+、.f-（切换本地上下文）
description: F. + 命令将帧索引转移到当前堆栈中的下一帧。 F-command 将帧索引转移到当前堆栈的上一个帧中。
keywords:
- 。 f +， (Shift 本地上下文) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .f+, .f- (Shift Local Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c3e7c34c48df66cc5ea8fc5237cd86de67884514
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819414"
---
# <a name="f-f--shift-local-context"></a>.f+、.f-（切换本地上下文）


**F. +** 命令将帧索引转移到当前堆栈中的下一帧。 **F-** command 将帧索引转移到当前堆栈的上一个帧中。

```dbgcmd
.f+  
.f-  
```

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关本地上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。 有关如何显示局部变量和其他与内存相关的命令的详细信息，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

*该帧* 指定 (作用域的本地上下文) 调试器用来解释局部变量

**F +** 和. f-命令是移动到当前堆栈中的下一个和上一个帧的快捷方式。 这些命令等效于以下 [**. 帧**](-frame--set-local-context-.md) 命令，但为了方便起见，已缩短了 **. f** 命令：

-   **。 f +** 与相同 **。 frame @ $frame + 1**。

-   **. f-** 与 **. frame @ $frame-1** 相同。

美元符号 ($) 将帧值标识为 [伪寄存器](pseudo-register-syntax.md)。 At 符号 ( @ 使调试器能够更快地访问该值，因为它会通知调试器字符串是寄存器还是伪寄存器。

当应用程序运行时，本地变量的意义取决于程序计数器的位置，因为此类变量的作用域只扩展到在其中定义的函数。 除非使用 **f +** 或 **. f-** command (或 [**. frame**](-frame--set-local-context-.md) 命令) ，否则调试器将 (堆栈上的当前帧) 作为本地上下文，使用当前函数的作用域。

*帧号* 是堆栈跟踪内堆栈帧的位置。 可以通过使用 [**k、kb、glm-kc-qnw、kd、kp、kp、kv (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令或 [调用窗口](calls-window.md)来查看此堆栈跟踪。  (当前帧的第一行) 表示帧号0。 后续行表示第1、2、3等帧号。

您可以将本地上下文设置为不同的堆栈帧，以查看新的本地变量信息。 但是，可用的实际变量取决于所执行的代码。

如果执行了任何程序，调试器会将本地上下文重置为程序计数器的范围。 如果更改了寄存器上下文，则本地上下文将重置为顶部堆栈帧。

 

 





