---
title: 进程
description: 该过程扩展显示有关指定进程或所有进程，其中包括 EPROCESS 块的信息。
ms.assetid: 57f55632-8320-47cc-8a20-5a2cf3b42b3a
keywords:
- Windows 调试进程
ms.date: 08/02/2018
topic_type:
- apiref
api_name:
- process
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2740945a72b1b77f7b4c6db84e8fca2b1e9567b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334355"
---
# <a name="process"></a>!process


！ 处理有关指定进程或所有进程，其中包括 EPROCESS 块扩展显示信息。

可以在内核模式调试期间仅使用此扩展。

语法

```dbgcmd
!process [/s Session] [/m Module] [Process [Flags]]
!process [/s Session] [/m Module] 0 Flags ImageName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_s_Session"></span><span id="_s_session"></span><span id="_S_SESSION"></span>**/s** **** *会话*  
指定拥有所需的进程的会话。

<span id="_m_Module"></span><span id="_m_module"></span><span id="_M_MODULE"></span>**/m** **** *模块*  
指定拥有所需的进程的模块。

<span id="_Process"></span><span id="_process"></span><span id="_PROCESS"></span> *Process*  
在目标计算机上指定的十六进制的地址或进程的进程 ID。

值*进程*确定是否 ！ 过程扩展显示进程地址或进程 ID。 如果*进程*省略了在任何版本的 Windows，调试器将显示仅有关当前的系统进程的数据。 如果*进程*为 0 并*ImageName*是省略，调试器将显示有关所有活动进程的信息。 如果指定-1*进程*显示有关当前进程的信息。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>*标志*  
指定要显示详细信息的级别。 *标志*可以是以下位的任意组合。 如果*标志*为 0，则显示只有少量的信息。 默认值而异的 Windows 版本和的值*进程*。 如果默认值是 0x3*进程*省略或如果*进程*为 0 或-1; 否则，默认值是 0xF。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示时间和优先级的统计信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
线程和事件的列表显示与该过程中，并等待，其关联状态。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示与该进程关联的线程的列表。 如果这是包含不带位 1 (0x2)，在单个行上显示每个线程。 如果这是随附位 1，与堆栈跟踪显示每个线程。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
 显示的寄信人地址和取消函数自变量的显示每个函数的堆栈指针。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
 设置此命令的持续时间的进程上下文等于指定的进程。 这会导致以更准确地显示的线程堆栈。 因为此标志等效于使用[ **.process/p /r** ](-process--set-process-context-.md)指定进程，将丢弃任何现有的用户模式模块列表。 如果*进程*为零，则调试器会显示所有进程，并且为每个更改的进程上下文。 如果您要仅显示单个进程并刷新其用户模式状态 (例如，对于 **.process/p /r**)，不需要使用此标志。 此标志才会与位 0 (0x1) 一起使用时生效。

<span id="ImageName"></span><span id="imagename"></span><span id="IMAGENAME"></span>*ImageName*  
指定要显示的进程的名称。 调试器将显示其可执行映像名匹配的所有进程*ImageName*。 映像名称必须与匹配 EPROCESS 块中。 一般情况下，这是调用启动进程，包括文件扩展名 (通常为.exe)，并截断后的第 15 个字符时可执行文件名称。 没有方法来指定包含空格的映像名称。 当*ImageName*指定，则*进程*必须为零。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Kdexts.dll

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


在内核模式下的进程的信息，请参阅[更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

以下是一种 **！ process 0 0**显示：

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

下表介绍了一些的元素 **！ process 0 0**输出。

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
<td align="left"><p>Word 进程后的八个字符的十六进制数是 EPROCESS 块的地址。 在前面的示例中的最后一项，进程地址是 0x809258E0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>进程 ID (PID)</p></td>
<td align="left"><p>Word Cid 后面的十六进制数字。 在前面的示例中的最后一项，PID 是 0x44，或十进制 68。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>进程环境块 (PEB)</p></td>
<td align="left"><p>Word Peb 后面的十六进制数字是进程环境块的地址。 在前面的示例中的最后一项，PEB 位于地址 0x7FFDE000。</p></td>
</tr>
<tr class="even">
<td align="left"><p>父进程的 PID</p></td>
<td align="left"><p>十六进制数后 word ParentCid 是父进程的 PID。 在上述示例中，父进程的 PID 是 0x26 中的最后一项或十进制 38。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Image</p></td>
<td align="left"><p>拥有进程的模块的名称。 在前面的示例中的最后一项，所有者是 spoolss.exe。 在第一个项，所有者是操作系统本身。</p></td>
</tr>
<tr class="even">
<td align="left"><p>进程对象地址</p></td>
<td align="left"><p>Word 对象表后面的十六进制数字。 在前面的示例中的最后一项，进程对象的地址是 0x80925c68。</p></td>
</tr>
</tbody>
</table>

 

若要显示上一个过程的完整详细信息，请设置*标志*到 7。 可以通过设置指定的进程本身*进程*等于设置的进程地址*进程*等于的进程 ID 或设置*ImageName*等于可执行映像名称。 下面是一个示例：

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

请注意，进程对象的地址可以用作输入到其他扩展，如[ **！ 处理**](-handle.md)，以获取进一步的信息。

下表介绍了一些在上一示例中的元素。

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
<td align="left">等待</td>
<td align="left">此标题之后插入的注释提供了在等待的原因。 该命令<strong><a href="dt--display-type-.md" data-raw-source="[dt nt!_KWAIT_REASON](dt--display-type-.md)">dt nt ！ _KWAIT_REASON</a></strong>将显示所有的等待原因的列表。</td>
</tr>
<tr class="even">
<td align="left"><p>ElapsedTime</p></td>
<td align="left"><p>列出自创建该过程以来已经过去的时间量。 这被显示在 Hours:Minutes:Seconds.Milliseconds 单位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UserTime</p></td>
<td align="left"><p>列出进程已在用户模式下运行的时间量。 如果值为 UserTime 极大，它可能会标识会耗尽系统资源的进程。 单位为那些 ElapsedTime 相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KernelTime</p></td>
<td align="left"><p>列出进程已在内核模式下运行的时间量。 如果值为 KernelTime 极大，它可能会标识会耗尽系统资源的进程。 单位为那些 ElapsedTime 相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>工作集大小</p></td>
<td align="left"><p>列出了该过程中，在页面中的当前、 最小和最大工作集大小。 极大的工作集大小可以是进程的正在泄漏内存或耗尽系统资源的符号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>QuotaPoolUsage 条目</p></td>
<td align="left"><p>列出了由进程使用的分页和非分页池。 在系统上的内存泄漏，观察所有进程过多的非分页缓冲的池使用率可以告诉您哪些进程拥有内存泄漏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>克隆</p></td>
<td align="left"><p>指示过程已通过 POSIX 或 Interix 子系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Private</p></td>
<td align="left"><p>指示进程当前使用的专用 （非共享） 页面数。 这包括在分页和内存分页。</p></td>
</tr>
</tbody>
</table>

 

除了进程列表信息中，线程信息包含在线程在其拥有锁的资源的列表。 线程标头之后，如果第三行输出中列出此信息。 在此示例中，线程具有对一个资源，且地址 80144 fc 0 为同步事件的锁定。 通过将此地址的情况下显示的锁的列表进行比较[ **！ kdext\*.locks** ](-locks---kdext--locks-.md)扩展，您可以确定哪些线程资源具有排他锁。

[ **！ 堆栈**](-stacks.md)扩展为提供的每个线程的状态的简短摘要。 这可以使用而不是 ！ 处理扩展以获取系统的快速概述，尤其是在调试多线程问题，例如资源冲突或死锁。

 

 





