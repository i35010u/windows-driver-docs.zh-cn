---
title: .frame（设置本地上下文）
description: Frame 命令指定哪个本地上下文 (范围) 用于解释局部变量或显示当前的本地上下文。
keywords:
- " ( 设置本地上下文) 命令"
- 内存，将本地上下文设置 (。) 命令
- context， (，请设置本地上下文) 命令
- 。 frame (设置本地上下文) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .frame (Set Local Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b369fa190a6e1c044b3b782a77bc09cff862ee70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821067"
---
# <a name="frame-set-local-context"></a>.frame（设置本地上下文）


**Frame** 命令指定哪个本地上下文 (范围) 用于解释局部变量或显示当前的本地上下文。

```dbgcmd
.frame [/c] [/r] [FrameNumber] 
.frame [/c] [/r] = BasePtr [FrameIncrement] 
.frame [/c] [/r] = BasePtr StackPtr InstructionPtr 
```

## <a name="span-idddk_meta_set_local_context_dbgspanspan-idddk_meta_set_local_context_dbgspanparameters"></a><span id="ddk_meta_set_local_context_dbg"></span><span id="DDK_META_SET_LOCAL_CONTEXT_DBG"></span>参数


<span id="________c______"></span><span id="________C______"></span>**/c**   
将指定的帧设置为当前的本地重写上下文。 此操作允许用户访问调用堆栈中任何函数的非易失性寄存器。

<span id="________r______"></span><span id="________R______"></span>**/r**   
显示有关指定的本地上下文的寄存器和其他信息。

<span id="_______FrameNumber______"></span><span id="_______framenumber______"></span><span id="_______FRAMENUMBER______"></span>*FrameNumber*   
指定所需的本地上下文的帧数。 如果此参数为零，则该命令将指定当前帧。 如果省略此参数，则此命令将显示当前的本地上下文。

<span id="_______BasePtr______"></span><span id="_______baseptr______"></span><span id="_______BASEPTR______"></span>*BasePtr*   
指定用于确定帧的堆栈跟踪的基指针（如果在命令名称后面添加一个等号 (=)  (") **。** 在基于 x86 的处理器上，在 (*BasePtr* 之后添加另一个参数，该参数被解释为 *FrameIncrement*) 或 *BasePtr* (后两个以上的参数，这些参数被解释为 *InstructionPtr* 和 *StackPtr*) 。

<span id="_______FrameIncrement______"></span><span id="_______frameincrement______"></span><span id="_______FRAMEINCREMENT______"></span>*FrameIncrement*   
仅)  (基于 x86 的处理器

指定超出基指针的其他帧数量。 例如，如果基指针0x0012FF00 是第3帧的地址，则命令 **。 frame 12ff00** 等效于 **. 帧 3**，和 **。 frame 12ff00 2** 等效于 **。帧 5**。

<span id="_______StackPtr______"></span><span id="_______stackptr______"></span><span id="_______STACKPTR______"></span>*StackPtr*   
仅)  (基于 x86 的处理器指定用于确定帧的堆栈跟踪的堆栈指针。 如果忽略 *StackPtr* 和 *InstructionPtr*，则调试器将使用 **esp** register 指定的堆栈指针和 **eip** 注册指定的指令指针。

<span id="_______InstructionPtr______"></span><span id="_______instructionptr______"></span><span id="_______INSTRUCTIONPTR______"></span>*InstructionPtr*   
仅)  (基于 x86 的处理器指定用于确定帧的堆栈跟踪的指令指针。 如果忽略 *StackPtr* 和 *InstructionPtr*，则调试器将使用 **esp** register 指定的堆栈指针和 **eip** 注册指定的指令指针。

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

当应用程序运行时，本地变量的意义取决于程序计数器的位置，因为此类变量的作用域只扩展到在其中定义的函数。 如果不使用 **frame** 命令，调试器将使用当前函数的作用域 (堆栈上的当前帧) 为 [本地上下文](changing-contexts.md#local-context)。

若要更改本地上下文，请使用 **frame** 命令并指定所需的帧号。

*帧号* 是堆栈跟踪内堆栈帧的位置。 可以通过 [**k (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令或 [调用窗口](calls-window.md)来查看此堆栈跟踪。 当前帧 (第一行) 为帧号0。 后续行表示第1、2、3等帧号。

如果将 **n** 参数与 [**k**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令一起使用，则 **k** 命令会将帧号与堆栈跟踪一起显示。 这些帧号始终以十六进制格式显示。 另一方面，如果使用前缀（如0x）覆盖此设置，则 **frame** 命令会将其参数解释为默认基数。 若要更改默认基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。

您可以将本地上下文设置为不同的堆栈帧，以便您可以查看新的本地变量信息。 但是，可用的实际变量取决于正在执行的代码。

如果执行任何应用程序，则本地上下文将重置为程序计数器的范围。 如果更改了寄存器上下文，则本地上下文将重置为顶部堆栈帧。

 

 





