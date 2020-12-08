---
title: 进程
description: 进程扩展显示有关指定进程或所有进程的信息，包括 EPROCESS 块。
keywords:
- 处理 Windows 调试
ms.date: 08/02/2018
topic_type:
- apiref
api_name:
- process
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ecbc21437b6baa3efa222b9777f9714bebaa421d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792007"
---
# <a name="process"></a>!process


！进程扩展显示有关指定进程或所有进程的信息，包括 EPROCESS 块。

此扩展只能在内核模式调试过程中使用。

语法

```dbgcmd
!process [/s Session] [/m Module] [Process [Flags]]
!process [/s Session] [/m Module] 0 Flags ImageName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_s_Session"></span><span id="_s_session"></span><span id="_S_SESSION"></span>**/s**  **** *会话*  
指定拥有所需进程的会话。

<span id="_m_Module"></span><span id="_m_module"></span><span id="_M_MODULE"></span>**/m**  **** *模块*  
指定拥有所需进程的模块。

<span id="_Process"></span><span id="_process"></span><span id="_PROCESS"></span>*处理*  
指定目标计算机上的十六进制地址或进程的进程 ID。

*Process* 的值确定！进程扩展是否显示进程地址或进程 ID。 如果在任何版本的 Windows 中省略 *进程* ，则调试器只显示有关当前系统进程的数据。 如果 *Process* 为0并且省略 *ImageName* ，则调试器将显示所有活动进程的相关信息。 如果指定-1，则显示有关当前进程的 *进程* 信息。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>*随意*  
指定要显示的详细信息的级别。 *标志* 可以是以下位的任意组合。 如果 *Flags* 为0，则只显示最少数量的信息。 默认值因 Windows 版本和 *进程* 的值而异。 如果省略了 *进程* ，或者 *进程* 为0或-1，则默认值为 0x3;否则，默认值为0xF。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示时间和优先级统计信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示与进程关联的线程和事件的列表及其等待状态。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示与进程关联的线程的列表。 如果包含此项时没有位 1 (0x2) ，则每个线程都显示在一行上。 如果此项与位1一起包含，则每个线程都将显示堆栈跟踪。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
 显示每个函数的返回地址和堆栈指针是否隐含函数参数显示。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
 在此命令的持续时间内将进程上下文设置为等于指定进程。 这将导致更准确地显示线程堆栈。 由于此标志等效于使用为指定进程 [**处理/p/r**](-process--set-process-context-.md) ，因此将丢弃任何现有的用户模式模块列表。 如果 *进程* 为零，调试器将显示所有进程，并更改每个进程的进程上下文。 如果你只显示一个进程，并且其用户模式状态已刷新 (例如，使用 **. process/p/r**) ，则无需使用此标志。 此标志仅在与位 0 (0x1) 一起使用时才有效。

<span id="ImageName"></span><span id="imagename"></span><span id="IMAGENAME"></span>*ImageName*  
指定要显示的进程的名称。 调试器将显示可执行映像名称与 *ImageName* 匹配的所有进程。 映像名称必须与 EPROCESS 块中的名称匹配。 通常，这是用于启动进程的可执行文件名称，包括文件扩展名 (通常 .exe) ，并在第15个字符之后截断。 没有办法指定包含空格的图像名称。 指定 *ImageName* 时， *进程* 必须为零。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Kdexts.dll

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


有关内核模式下的进程的信息，请参阅 [更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。

<a name="remarks"></a>备注
-------

下面是 **！ process 0 0** 显示的一个示例：

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
PROCESS 80a02a60  Cid: 0002    Peb: 00000000  ParentCid: 0000
    DirBase: 00006e05  ObjectTable: 80a03788  TableSize: 150.
    Image: System
PROCESS 80986f40  Cid: 0012    Peb: 7ffde000  ParentCid: 0002
    DirBase: 000bd605  ObjectTable: 8098fce8  TableSize:  38.
    Image: smss.exe
PROCESS 80958020  Cid: 001a    Peb: 7ffde000  ParentCid: 0012
    DirBase: 0008b205  ObjectTable: 809782a8  TableSize: 150.
    Image: csrss.exe
PROCESS 80955040  Cid: 0020    Peb: 7ffde000  ParentCid: 0012
    DirBase: 00112005  ObjectTable: 80955ce8  TableSize:  54.
    Image: winlogon.exe
PROCESS 8094fce0  Cid: 0026    Peb: 7ffde000  ParentCid: 0020
    DirBase: 00055005  ObjectTable: 80950cc8  TableSize: 222.
    Image: services.exe
PROCESS 8094c020  Cid: 0029    Peb: 7ffde000  ParentCid: 0020
    DirBase: 000c4605  ObjectTable: 80990fe8  TableSize: 110.
    Image: lsass.exe
PROCESS 809258e0  Cid: 0044    Peb: 7ffde000  ParentCid: 0026
    DirBase: 001e5405  ObjectTable: 80925c68  TableSize:  70.
    Image: SPOOLSS.EXE
```

下表描述了 **！ process 0 0** 输出的某些元素。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">元素</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>进程地址</p></td>
<td align="left"><p>单词进程后8个字符的十六进制数字是 EPROCESS 块的地址。 在上一示例的最后一项中，进程地址为0x809258E0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>进程 ID (PID) </p></td>
<td align="left"><p>单词 Cid 后面的十六进制数。 在前面的示例的最后一项中，PID 为0x44 或 decimal 68。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>进程环境块 (PEB) </p></td>
<td align="left"><p>单词 Peb 后面的十六进制数是进程环境块的地址。 在上一示例的最后一项中，PEB 位于 address 0x7FFDE000。</p></td>
</tr>
<tr class="even">
<td align="left"><p>父进程 PID</p></td>
<td align="left"><p>单词 ParentCid 后面的十六进制数字是父进程的 PID。 在上一示例的最后一项中，父进程 PID 为0x26 或 decimal 38。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>映像</p></td>
<td align="left"><p>拥有进程的模块的名称。 在前面的示例中的最后一项，spoolss.exe 所有者。 第一项是操作系统本身。</p></td>
</tr>
<tr class="even">
<td align="left"><p>处理对象地址</p></td>
<td align="left"><p>单词 ObjectTable 后面的十六进制数。 在前面的示例的最后一项中，进程对象的地址为0x80925c68。</p></td>
</tr>
</tbody>
</table>

 

若要在一个进程中显示完整的详细信息，请将 *标志* 设置为7。 可以通过将 " *进程* " 设置为 "进程地址"，将 " *进程* " 设置为等于进程 ID，或将 " *ImageName* " 设置为等于可执行映像名称来指定进程本身。 以下是示例：

```dbgcmd
kd> !process fb667a00 7
PROCESS fb667a00 Cid: 0002  Peb: 00000000 ParentCid: 0000
  DirBase: 00030000 ObjectTable: e1000f88 TableSize: 112.
  Image: System
  VadRoot fb666388 Clone 0 Private 4. Modified 9850. Locked 0.
  FB667BBC MutantState Signalled OwningThread 0
  Token               e10008f0
  ElapsedTime            15:06:36.0338
  UserTime             0:00:00.0000
  KernelTime            0:00:54.0818
  QuotaPoolUsage[PagedPool]     1480
Working Set Sizes (now,min,max) (3, 50, 345)
  PeakWorkingSetSize        118
  VirtualSize            1 Mb
  PeakVirtualSize          1 Mb
  PageFaultCount          992
  MemoryPriority          BACKGROUND
  BasePriority           8
  CommitCharge           8

    THREAD fb667780 Cid 2.1 Teb: 00000000 Win32Thread: 80144900 WAIT: (WrFreePage) KernelMode Non-Alertable
    80144fc0 SynchronizationEvent
    Not impersonating
    Owning Process fb667a00
    WaitTime (seconds)   32278
    Context Switch Count  787
    UserTime         0:00:00.0000
    KernelTime        0:00:21.0821
    Start Address Phase1Initialization (0x801aab44)
    Initial Sp fb26f000 Current Sp fb26ed00
    Priority 0 BasePriority 0 PriorityDecrement 0 DecrementCount 0

    ChildEBP RetAddr Args to Child
    fb26ed18 80118efc c0502000 804044b0 00000000 KiSwapThread+0xb5
    fb26ed3c 801289d9 80144fc0 00000008 00000000 KeWaitForSingleObject+0x1c2
```

请注意，process 对象的地址可用作其他扩展的输入，例如 [**！ handle**](-handle.md)，以获取更多信息。

下表描述了上一示例中的某些元素。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">元素</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WAIT</td>
<td align="left">此标题后的括号注释提供等待的原因。 命令 <strong><a href="dt--display-type-.md" data-raw-source="[dt nt!_KWAIT_REASON](dt--display-type-.md)">dt nt！ _KWAIT_REASON</a></strong> 将显示所有等待原因的列表。</td>
</tr>
<tr class="even">
<td align="left"><p>ElapsedTime</p></td>
<td align="left"><p>列出自创建进程以来所经过的时间。 以小时为单位显示：分钟：秒。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UserTime</p></td>
<td align="left"><p>列出进程在用户模式下运行的时间。 如果 UserTime 的值过高，则可能会识别耗尽系统资源的进程。 单位与 ElapsedTime 的单位相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KernelTime</p></td>
<td align="left"><p>列出进程在内核模式下运行的时间。 如果 KernelTime 的值过高，则可能会识别耗尽系统资源的进程。 单位与 ElapsedTime 的单位相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>工作集大小</p></td>
<td align="left"><p>列出进程的当前、最小和最大工作集大小（以页为限）。 特别大的工作集大小可以是泄漏内存或耗尽系统资源的进程的符号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>QuotaPoolUsage 条目</p></td>
<td align="left"><p>列出进程使用的分页和非分页池。 在出现内存泄漏的系统上，在所有进程上查找过多的非分页池使用情况会告诉你哪个进程存在内存泄漏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>克隆</p></td>
<td align="left"><p>指示进程是否由 POSIX 或 Interix 子系统创建。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Private</p></td>
<td align="left"><p>指示进程当前正在使用的) 专用 (不可共享的页的数目。 这包括分页进和分页出内存。</p></td>
</tr>
</tbody>
</table>

 

除了进程列表信息之外，线程信息还包含线程在其上锁定的资源的列表。 此信息在线程标头后的输出的第三行中列出。 在此示例中，该线程在一个资源上有一个锁，SynchronizationEvent 地址为80144fc0。 通过将此地址与 [**！ kdext \***](-locks---kdext--locks-.md) 扩展显示的锁列表进行比较，可以确定哪些线程具有对资源的独占锁。

[**！**](-stacks.md) Stack 扩展提供每个线程的状态的简短摘要。 这可以用来代替！进程扩展来快速概述系统，尤其是在调试多线程问题时（例如资源冲突或死锁）。

 

 





