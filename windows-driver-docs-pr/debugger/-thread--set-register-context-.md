---
title: .thread（设置寄存器上下文）
description: Thread 命令指定将用于寄存器上下文的线程。
keywords:
- 设置寄存器上下文 () 命令
- context，将注册上下文设置 ( 的) 命令
- 注册，设置寄存器上下文 () 命令
- 调用堆栈， ( 中设置注册上下文) 命令
- 。线程 (设置注册上下文) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .thread (Set Register Context)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 931b76d88ed43d86b7d96be9d4e2747608a9ce2a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830309"
---
# <a name="thread-set-register-context"></a>.thread（设置寄存器上下文）


**Thread** 命令指定将用于寄存器上下文的线程。

```dbgcmd
.thread [/p [/r] ] [/P] [/w] [Thread]
```

## <a name="span-idddk_meta_set_register_context_dbgspanspan-idddk_meta_set_register_context_dbgspanparameters"></a><span id="ddk_meta_set_register_context_dbg"></span><span id="DDK_META_SET_REGISTER_CONTEXT_DBG"></span>参数


<span id="________p______"></span><span id="________P______"></span>**/p**   
 (实时调试仅) 如果包括此选项并且 *Thread* 为非零，则拥有此线程的进程 (pte) 的所有转换页表项将在访问之前自动转换为物理地址。 这可能会导致速度降低，因为调试器必须查找此进程使用的所有内存的物理地址，并且可能需要跨调试电缆传输大量数据。  (此行为与的 forcedecodeuser。 ) [**缓存**](-cache--set-cache-size-.md)。

如果包含 **/p** 选项并且 *Thread* 为零或省略，则将禁用此转换。  (此行为与的 noforcedecodeuser。 ) [**缓存**](-cache--set-cache-size-.md)。

<span id="________r______"></span><span id="________R______"></span>**/r**   
 (实时调试仅) 如果 **/r** 选项随 **/p** 选项一起提供，则拥有此线程的进程的用户模式符号将在设置了进程和注册上下文后重新加载。  (此行为与的相同 [**。重载/user**](-reload--reload-module-.md)。 ) 

<span id="________P______"></span><span id="________p______"></span>**/P**   
 (实时调试仅) 如果包括此选项并且 *Thread* 为非零，则在访问之前， (pte) 的所有转换页表项都将自动转换为物理地址。 不同于 **/p** 选项，这会转换所有用户模式和内核模式进程的 pte，而不仅是拥有此线程的进程。 这可能会导致速度降低，因为调试程序必须查找所有正在使用的内存的物理地址，并且可能需要跨调试电缆传输大量的数据。  (此行为与的 forcedecodeptes。 ) [**缓存**](-cache--set-cache-size-.md)。

<span id="________w______"></span><span id="________W______"></span>**/w**   
 (64 位内核调试仅) 将线程的活动上下文更改为 WOW64 32 位上下文。 指定的线程必须在具有 WOW64 状态的进程中运行。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
线程的地址。 如果省略或为零，则线程上下文将重置为当前线程。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关注册上下文和其他上下文设置的详细信息，请参阅 [更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

通常，在执行内核调试时，唯一可见的寄存器与当前线程关联。

**Thread** 命令指示内核调试器使用指定的线程作为寄存器上下文。 执行此命令后，调试器将有权访问此线程的最重要寄存器和堆栈跟踪。 此注册上下文会一直保留，直到你允许目标执行或使用另一个寄存器上下文 **.thread** 命令 (。 [**.cxr**](-cxr--display-context-record-.md)[**或) 。**](-trap--display-trap-frame-.md) 有关完整详细信息，请参阅 [注册上下文](changing-contexts.md#register-context) 。

**/W** 选项只能在具有 WOW64 状态的进程中运行的线程上的64位内核调试会话中使用。 检索到的上下文将是 WOW64 记住的最后一个上下文;这通常是 *线程* 执行的最后一个用户模式代码。 仅当目标为纯计算机模式时，才可以使用此选项。 例如，如果目标运行在使用 WOW64 模拟基于 x86 的处理器的64位计算机上，则不能使用此选项。 使用 **/w** 选项将导致计算机模式自动切换到基于 x86 的处理器。

此命令并不实际更改当前线程。 换言之，如果没有与参数一起 [**使用的任何**](-thread.md) 参数 [**，则这些扩展将仍**](-teb.md) 默认为当前线程。

示例如下。 使用 [**！进程**](-process.md) 扩展查找所需线程的地址。  (在本例中， **！ process 0 0** 用于列出所有进程，然后再次使用 **！进程** 来列出所需进程的所有线程。 ) 

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

现在，使用带有所需线程地址的 **. thread** 命令。 这将设置寄存器上下文，并使你能够检查重要寄存器以及此线程的调用堆栈。

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

 

 





