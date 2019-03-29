---
title: .f+、.f-（切换本地上下文）
description: .F + 命令移至下一帧中当前堆栈帧索引。 .F 命令会切换到上一个在当前堆栈帧的帧索引。
ms.assetid: aade5ec0-4d40-4ff1-9d4b-f3ad81b54b79
keywords:
- .f +，.f-（shift 本地上下文） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .f+, .f- (Shift Local Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7dff1469610c6659ceb2b7a1d9003cd93bfa07c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577109"
---
# <a name="f-f--shift-local-context"></a>.f+、.f-（切换本地上下文）


**.F +** 命令会将帧索引移动到当前堆栈中的下一帧。 **.F-** 命令会将帧索引移动到当前堆栈中的上一帧。

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关本地上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。 有关如何显示本地变量和其他与内存相关的命令的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

*帧*指定调试器使用来解释本地变量的本地上下文 （作用域）

**.F +** 和.f 命令是将移动到当前堆栈中的下一步和上一个帧的快捷方式。 这些命令是等效于以下[ **.frame** ](-frame--set-local-context-.md)命令，但 **.f**命令都是为方便起见较短：

-   **.f +** 等同于 **.frame @$ 帧 + 1**。

-   **.f-** 等同于 **.frame @$ 帧-1**。

美元符号 （$） 标识在帧的值作为[伪寄存器](pseudo-register-syntax.md)。 At 符号 （@ 使调试器更快地访问值，因为它通知调试器字符串是注册或伪寄存器。

当运行应用程序时，本地变量的含义取决于位置的程序计数器，因为此类变量的作用域仅到函数中定义的扩展。 除非使用 **.f +** 或 **.f-** 命令 (或[ **.frame** ](-frame--set-local-context-.md)命令)，调试器使用的当前函数 （当前作用域在堆栈上的帧） 作为本地上下文。

*帧号*是堆栈跟踪内的堆栈帧的位置。 可以通过查看此堆栈跟踪[ **k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令或[调用窗口](calls-window.md)。 第一行 （当前帧） 表示的帧数 0。 后续行表示框架的数字 1，2，3，依此类推。

您可以将本地上下文设置为一个不同的堆栈帧以查看新的本地变量信息。 但是，可用的实际变量取决于执行的代码。

调试器重置本地上下文与程序计数器的作用域如果出现任何程序执行。 本地上下文是重置为顶级堆栈帧，如果更改寄存器上下文。

 

 





