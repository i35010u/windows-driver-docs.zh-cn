---
title: .frame （设置本地上下文）
description: .Frame 命令指定使用哪些本地上下文 （作用域） 来解释本地变量，或显示当前的本地上下文。
ms.assetid: eb843712-204f-4bbd-b711-a10756c9279a
keywords:
- 设置本地上下文 (.frame) 命令
- 内存中，设置本地上下文 (.frame) 命令
- 上下文中，设置本地上下文 (.frame) 命令
- .frame （设置本地上下文） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .frame (Set Local Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed2e2c3306edd234b46b96ba3f4ded323a545da7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526669"
---
# <a name="frame-set-local-context"></a>.frame （设置本地上下文）


**.Frame**命令指定使用哪些本地上下文 （作用域） 来解释本地变量，或显示当前的本地上下文。

```dbgcmd
.frame [/c] [/r] [FrameNumber] 
.frame [/c] [/r] = BasePtr [FrameIncrement] 
.frame [/c] [/r] = BasePtr StackPtr InstructionPtr 
```

## <a name="span-idddkmetasetlocalcontextdbgspanspan-idddkmetasetlocalcontextdbgspanparameters"></a><span id="ddk_meta_set_local_context_dbg"></span><span id="DDK_META_SET_LOCAL_CONTEXT_DBG"></span>参数


<span id="________c______"></span><span id="________C______"></span> **/c**   
为当前的本地替代上下文设置为指定的框架。 此操作允许用户访问调用堆栈中的任何函数的非易失性寄存器。

<span id="________r______"></span><span id="________R______"></span> **/r**   
显示寄存器和指定的本地上下文有关的其他信息。

<span id="_______FrameNumber______"></span><span id="_______framenumber______"></span><span id="_______FRAMENUMBER______"></span> *FrameNumber*   
指定其所需的本地上下文的帧数。 如果此参数为零，则该命令指定当前帧。 如果省略此参数，此命令显示当前的本地上下文。

<span id="_______BasePtr______"></span><span id="_______baseptr______"></span><span id="_______BASEPTR______"></span> *BasePtr*   
在命令名称后指定用来确定框架中，如果您添加一个等号 （=） 的堆栈跟踪的基指针 (**.frame**)。 在基于 x86 的处理器上，添加另一个参数后的*BasePtr* (它解释为*FrameIncrement*) 或两个多个参数之后*BasePtr* （它们是解释为*InstructionPtr*并*StackPtr*)。

<span id="_______FrameIncrement______"></span><span id="_______frameincrement______"></span><span id="_______FRAMEINCREMENT______"></span> *FrameIncrement*   
（仅限基于 x86 处理器）

指定过去的基指针的帧的额外数量。 例如，如果基指针 0x0012FF00 为帧 3，该命令的地址 **.frame 12ff00**等效于 **.frame 3**，并 **.frame 12ff00 2**等效于 **.frame 5**。

<span id="_______StackPtr______"></span><span id="_______stackptr______"></span><span id="_______STACKPTR______"></span> *StackPtr*   
（仅限基于 x86 处理器）指定用于确定帧的堆栈跟踪的堆栈指针。 如果省略*StackPtr*并*InstructionPtr*，调试器使用的堆栈指针的**esp**注册指定和指令指针的**eip**注册指定。

<span id="_______InstructionPtr______"></span><span id="_______instructionptr______"></span><span id="_______INSTRUCTIONPTR______"></span> *InstructionPtr*   
（仅限基于 x86 处理器）指定用于确定帧的堆栈跟踪中的指令指针。 如果省略*StackPtr*并*InstructionPtr*，调试器使用的堆栈指针的**esp**注册指定和指令指针的**eip**注册指定。

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

当运行应用程序时，本地变量的含义取决于位置的程序计数器，因为此类变量的作用域仅到函数中定义的扩展。 如果不使用 **.frame**命令时，调试器使用的当前函数 （在堆栈上当前的帧） 作用域作为[本地上下文](changing-contexts.md#local-context)。

若要更改本地上下文，请使用 **.frame**命令并指定所需的帧号码。

*帧号*是堆栈跟踪内的堆栈帧的位置。 您可以查看与此堆栈跟踪[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令或[调用窗口](calls-window.md)。 第一行 （当前帧） 为帧号 0。 后续行表示框架的数字 1，2，3，依此类推。

如果您使用**n**参数与[ **k** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令， **k**命令显示以及堆栈跟踪的帧号码。 这些帧数字始终以十六进制格式显示。 但是， **.frame**命令将解释在默认基数，其自变量，除非重写此设置，但诸如 0x 之类的前缀。 若要更改默认基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。

您可以将本地上下文设置为不同的堆栈帧，以使您能够查看新的本地变量信息。 但是，可用的实际变量取决于正在执行的代码。

本地上下文与程序计数器的作用域是重置任何应用程序执行时。 本地上下文是重置为顶级堆栈帧，如果更改寄存器上下文。

 

 





