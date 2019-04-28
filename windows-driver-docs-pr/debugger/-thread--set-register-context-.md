---
title: .thread（设置寄存器上下文）
description: .Thread 命令指定的线程将用于寄存器上下文。
ms.assetid: 577276b7-a6c4-427e-ada1-10dbb62ebd5c
keywords:
- 设置注册上下文 (.thread) 命令
- 上下文中，设置注册上下文 (.thread) 命令
- 寄存器中，设置注册上下文 (.thread) 命令
- 调用堆栈，设置注册上下文 (.thread) 命令
- .thread （设置寄存器上下文） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .thread (Set Register Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5b875b72ad47b4b9c46ff79797518ee3e9b2702
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334200"
---
# <a name="thread-set-register-context"></a>.thread（设置寄存器上下文）


**.Thread**命令指定的线程将用于寄存器上下文。

```dbgcmd
.thread [/p [/r] ] [/P] [/w] [Thread]
```

## <a name="span-idddkmetasetregistercontextdbgspanspan-idddkmetasetregistercontextdbgspanparameters"></a><span id="ddk_meta_set_register_context_dbg"></span><span id="DDK_META_SET_REGISTER_CONTEXT_DBG"></span>参数


<span id="________p______"></span><span id="________P______"></span> **/p**   
（仅限调试实时）如果包括此选项则和*线程*为非零值，所有过渡页表项 (Pte) 拥有此线程的进程将自动都转换为之前访问的物理地址。 这可能导致速度变慢，因为调试程序将需要查找所有此过程中，使用的内存的物理地址，并且可能需要大量的数据必须调试缆线传输。 (此行为是相同的[ **.cache forcedecodeuser**](-cache--set-cache-size-.md)。)

如果 **/p**已包含选项和*线程*为零或省略，就将禁用这种转换。 (此行为是相同的[ **.cache noforcedecodeuser**](-cache--set-cache-size-.md)。)

<span id="________r______"></span><span id="________R______"></span> **/r**   
（仅限调试实时）如果 **/r**已以及包含选项 **/p**选项，用户模式下将在设置过程和寄存器上下文之后重新加载此线程的进程拥有的符号。 (此行为是相同的[ **.reload /user**](-reload--reload-module-.md)。)

<span id="________P______"></span><span id="________p______"></span> **/P**   
（仅限调试实时）如果包括此选项则和*线程*为非零值，所有过渡页表项 (Pte) 将自动都转换为之前访问的物理地址。 与不同 **/p**选项，这会转换为所有用户模式和内核模式进程，Pte 而不仅仅是拥有此线程的进程。 这可能导致速度变慢，因为调试程序将需要查找在使用中，所有内存的物理地址，并且可能需要跨调试缆线传输大量数据。 (此行为是相同的[ **.cache forcedecodeptes**](-cache--set-cache-size-.md)。)

<span id="________w______"></span><span id="________W______"></span> **/w**   
（仅限调试 64 位内核）更改为的 WOW64 32 位上下文线程的活动上下文。 必须在具有 WOW64 状态的进程中运行指定的线程。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
线程的地址。 如果省略该步骤或零，线程上下文重置为当前线程。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>内核模式下</p></td>
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

有关寄存器上下文和其他上下文设置的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

通常情况下，执行内核调试，仅在可见寄存器时，与当前线程关联的对象。

**.Thread**命令指示内核调试程序，用于指定的线程寄存器上下文。 执行此命令后，调试器将具有访问此线程的最重要的寄存器和堆栈跟踪。 允许目标以执行或使用另一个寄存器上下文命令之前将一直保留此寄存器上下文 (**.thread**， [ **.cxr**](-cxr--display-context-record-.md)，或[ **.trap**](-trap--display-trap-frame-.md))。 请参阅[注册上下文](changing-contexts.md#register-context)有关完整详细信息。

**/W**选项只能在 64 位内核调试具有 WOW64 状态的进程中运行的线程上的会话中。 检索的上下文将记住 WOW64; 的最后一个上下文这通常是由执行的最后一个用户模式代码*线程*。 如果目标是在本机模式下，仅可以使用此选项。 例如，如果目标模拟使用 WOW64 的基于 x86 的处理器的 64 位计算机上运行，则不能使用此选项。 使用 **/w**选项将导致计算机模式下，若要自动切换到基于 x86 的处理器。

此命令实际上不会更改当前线程。 换而言之，扩展，例如[ **！ 线程**](-thread.md)并[ **！ teb** ](-teb.md)仍将默认为当前线程，如果没有自变量用于它们。

下面是一个示例。 使用[ **！ 过程**](-process.md)扩展来查找所需线程的地址。 (在这种情况下， **！ process 0 0**用于列出的所有进程，然后 **！ 过程**用于第二次都列出所需的进程的所有线程。)

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
PROCESS fe5039e0  SessionId: 0  Cid: 0008    Peb: 00000000  ParentCid: 0000
    DirBase: 00030000  ObjectTable: fe529a88  TableSize: 145.
    Image: System

.....

PROCESS ffaa5280  SessionId: 0  Cid: 0120    Peb: 7ffdf000  ParentCid: 01e0
    DirBase: 03b70000  ObjectTable: ffaa4e48  TableSize:  23.
    Image: winmine.exe

kd> !process ffaa5280
PROCESS ffaa5280  SessionId: 0  Cid: 0120    Peb: 7ffdf000  ParentCid: 01e0
    DirBase: 03b70000  ObjectTable: ffaa4e48  TableSize:  23.
    Image: winmine.exe
    VadRoot ffaf6e48 Clone 0 Private 50. Modified 0. Locked 0.
    DeviceMap fe502e88
    Token                             e1b55d70

.....

        THREAD ffaa43a0  Cid 120.3a4  Teb: 7ffde000  Win32Thread: e1b4fea8 WAIT: (WrUserRequest) UserMode Non-Alertable
            ffadc6a0  SynchronizationEvent
        Not impersonating
        Owning Process ffaa5280
        WaitTime (seconds)      24323
        Context Switch Count    494                   LargeStack

.....
```

现在，使用 **.thread**命令所需线程的地址。 此设置寄存器上下文，并可以检查重要寄存器和此线程的调用堆栈。

```dbgcmd
kd> .thread ffaa43a0
Using context of thread ffaa43a0

kd> r
Last set context:
eax=00000000 ebx=00000000 ecx=00000000 edx=00000000 esi=00000000 edi=00000000
eip=80403a0d esp=fd581c2c ebp=fd581c60 iopl=0         nv up di pl nz na pe nc
cs=0000  ss=0000  ds=0000  es=0000  fs=0000  gs=0000             efl=00000000
0000:3a0d ??              ???

kd> k
  *** Stack trace for last set context - .thread resets it
ChildEBP RetAddr  
fd581c38 8042d61c ntoskrnl!KiSwapThread+0xc5
00001c60 00000000 ntoskrnl!KeWaitForSingleObject+0x1a1
```

 

 





