---
title: Bug 检查 0x50 PAGE_FAULT_IN_NONPAGED_AREA
description: PAGE_FAULT_IN_NONPAGED_AREA bug 检查具有 0x00000050 值。 这表示已引用无效的系统内存。
ms.assetid: 63b4ab82-f7a9-4e14-bf7c-707a22d7e251
keywords:
- Bug 检查 0x50 PAGE_FAULT_IN_NONPAGED_AREA
- PAGE_FAULT_IN_NONPAGED_AREA
ms.date: 03/28/2017
topic_type:
- apiref
api_name:
- PAGE_FAULT_IN_NONPAGED_AREA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6edf37a1b28c4306dfb470000604ad1c51cc5f0f
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239064"
---
# <a name="bug-check-0x50-pagefaultinnonpagedarea"></a>Bug 检查 0x50：页\_容错\_IN\_未分页\_区域


页面\_容错\_IN\_未分页\_区域 bug 检查的值为 0x00000050。 这表示已引用无效的系统内存。 通常的内存地址是错误或内存地址指向已释放内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="pagefaultinnonpagedarea-parameters"></a>页\_容错\_IN\_未分页\_区域参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>引用的内存地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>读取操作</p>
<p><strong>1:</strong>写入操作</p>
<p><strong>2:</strong>执行操作</p>
<p><strong>8:</strong>执行操作</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>（如果已知） 引用内存的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>页面错误的类型</p>
<p>0x03-NONPAGED_BUGCHECK_WRONG_SESSION-对会话空间地址的尝试的引用已不有任何会话的进程的上下文中。  通常这意味着调用方未正确尝试访问会话地址，而正确地获取了正确的进程的对象引用和首次附加到它。 在 Windows 10 RS3 上次使用此执行错误检查和子类型。  在 Windows 10 RS4 及更高版本，这是改为作为 0x02 (NONPAGED_BUGCHECK_NOT_PRESENT_PAGE_TABLE) 中出现错误。</p>
<p>0x04-NONPAGED_BUGCHECK_VA_NOT_CANONICAL-尝试对非规范化的 （非法） 虚拟地址 (参数 1) 的尝试的引用。  调用方应不曾经在尝试访问此地址。</p>
</td>
</tr>
</tbody>
</table>

 
如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。 可以使用调试器 dx 命令来显示此- `dx KiBugCheckDriver`。

<a name="cause"></a>原因
-----

Bug 检查 0x50 可能引起错误系统服务或有故障的驱动程序代码的安装。 防病毒软件也会触发此错误，如可能已损坏的 NTFS 卷。

它还可能会出现后安装的硬件故障或发生故障情况下安装的硬件 （通常与有缺陷的 RAM，是其主内存、 RAM L2 缓存或视频 RAM）。


<a name="remarks"></a>备注
----------

**事件日志中：** 检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

**解决错误的驱动程序：** 如果已显示在蓝色屏幕上或在事件日志中存在，请检查驱动程序的名称。 查看更新的驱动程序是否有可用的驱动程序供应商联系。 

**解决错误系统服务问题：** 禁用服务，并确认这会解决该错误。 如果是这样，请与系统服务有关的可能更新的制造商联系。 如果在系统启动期间发生错误，请调查 Windows 修复选项。 有关详细信息，请参阅[Windows 10 中的恢复选项](https://windows.microsoft.com/windows-10/windows-10-recovery-options)。

**在解决有关防病毒软件问题：** 禁用计划，并确认这会解决该错误。 如果是这样，请与联系有关可能的更新程序的制造商。

**在解决有关损坏的 NTFS 卷问题：** 运行**Chkdsk /f /r**以检测和修复磁盘错误。 系统分区上的磁盘扫描开始之前，必须重新启动系统。 请联系硬驱动程序系统查找任何诊断工具，它们为硬盘驱动器子系统提供的生产。

**Windows 内存诊断：** 运行 Windows 内存诊断工具，用于测试的物理内存。 单击开始按钮，然后单击控制面板。 在搜索框中，键入内存，然后依次*诊断您的计算机的内存问题*。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。

**解决硬件故障问题：** 如果硬件具有最近添加到系统，则删除它才能看到如果错误重复出现。 如果现有硬件出现故障，删除或更换有故障的组件。 应运行硬件诊断系统制造商提供。 有关这些过程的详细信息，请参阅您的计算机的所有者的手册。

有关常规的蓝色屏幕上，故障排除信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

<a name="resolution"></a>分辨率
----------

通常情况下，被引用的地址已释放的内存中，或只需无效。 这不会受到**试用-除**处理程序-它可以只是通过探测受保护或类似编程技术。

使用[ **！ 分析**](-analyze.md)调试扩展与-v verbose 选项以显示有关 bug 检查工作，以确定根本原因的信息。

```dbgcmd
2: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

PAGE_FAULT_IN_NONPAGED_AREA (50)
Invalid system memory was referenced.  This cannot be protected by try-except.
Typically the address is just plain bad or it is pointing at freed memory.
Arguments:
Arg1: ffffffff00000090, memory referenced.
Arg2: 0000000000000000, value 0 = read operation, 1 = write operation.
Arg3: fffff80240d322f9, If non-zero, the instruction address which referenced the bad memory
    address.
Arg4: 000000000000000c, (reserved)
```

在此示例中参数 2 指示 bug 检查发生时正在读取的内存区域。

查看所有 ！ 分析输出，以获取有关发生了什么信息上的 bug 检查发生的时间。 检查模块名： 和 FAULTING_MODULE： 若要查看哪些代码参与引用无效的系统内存。

在运行哪些程序发生失败时查看线索堆栈文本。 如果有多个转储文件，将信息查找是堆栈中的常见代码进行比较。

使用.trap 命令中提供 ！ 分析输出设置上下文。

```dbgcmd
TRAP_FRAME:  fffff98112e8b3d0 -- (.trap 0xfffff98112e8b3d0)
```

 使用调试器命令，例如使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)要调查的错误代码。

使用`lm t n`到内存中加载的模块列表。

使用[d、 da、 db、 dc、 dd、 dD、 df、 dp、 dq、 du，dw （显示内存）](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令要调查的参数 1 和 3 参数所引用的内存区域。

```dbgcmd
2: kd> db ffffffff00000090
ffffffff`00000090  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000a0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000b0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000c0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000d0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000e0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000f0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`00000100  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
```
在这种情况下并不像在参数 1，这是尝试读取内存的区域中的内存的此区域中没有数据。

使用[！ 地址](-address.md)命令以查看参数 3 的地址的引用的错误内存的指令。

```dbgcmd
2: kd> !address fffff80240d322f9
Usage:                  Module
Base Address:           fffff802`40ca8000
End Address:            fffff802`415fb000
Region Size:            00000000`00953000
VA Type:                BootLoaded
Module name:            ntoskrnl.exe
Module path:            [\SystemRoot\system32\ntoskrnl.exe]
```

使用[u、 ub、 uu （反汇编） Dissasemble](u--unassemble-.md)使用参数 3，检查其中引用错误的内存。 有关详细信息在 X64 上处理器和程序集语言请参见[x64 处理器](the-x64-processor.md)。 

```dbgcmd
2: kd> u fffff80240d322f9 
nt!RtlSubtreePredecessor+0x9:
fffff802`40d322f9 488b4810        mov     rcx,qword ptr [rax+10h]
fffff802`40d322fd eb07            jmp     nt!RtlSubtreePredecessor+0x16 (fffff802`40d32306)
fffff802`40d322ff 488bc1          mov     rax,rcx
fffff802`40d32302 488b4910        mov     rcx,qword ptr [rcx+10h]
fffff802`40d32306 4885c9          test    rcx,rcx
fffff802`40d32309 75f4            jne     nt!RtlSubtreePredecessor+0xf (fffff802`40d322ff)
fffff802`40d3230b c3              ret
fffff802`40d3230c c3              ret
```

使用`ub`到 dissassemble 向后从给定的地址。

使用[r （寄存器）](r--registers-.md)命令来检查作为检查系统错误时正在执行的内容。 

```dbgcmd
2: kd> r
Last set context:
rax=ffffffff00000080 rbx=0000000000000000 rcx=ffffa68337cb7028
rdx=7a107838c48dfc00 rsi=0000000000000000 rdi=0000000000000000
rip=fffff80240d322f9 rsp=ffff840c96510958 rbp=ffffffffffffffff
 r8=ffffffffffffffff  r9=0000000000000000 r10=7ffffffffffffffc
r11=ffff840c96510a10 r12=0000000000000000 r13=0000000000000000
r14=0000000000000000 r15=0000000000000000
iopl=0         nv up ei ng nz na pe nc
cs=0010  ss=0018  ds=0000  es=0000  fs=0000  gs=0000             efl=00010282
nt!RtlSubtreePredecessor+0x9:
fffff802`40d322f9 488b4810        mov     rcx,qword ptr [rax+10h] ds:ffffffff`00000090=????????????????
```

在这种情况下`fffff80240d322f9`指令指针中注册，翻录。

`!pte`和`!pool`命令还可用于检查内存。

使用`!memusage`并检查系统内存的一般状态。 

**驱动程序验证程序**

驱动程序验证程序是一种工具，运行实时检查驱动程序的行为。 例如，驱动程序验证工具将检查内存资源，如内存池的使用。 如果它发现错误的驱动程序代码执行过程中，它会主动创建例外以允许驱动程序代码以进行进一步仔细检查该部分。 驱动程序验证程序管理器内置于 Windows，可在所有 Windows Pc 上。 若要启动驱动程序验证程序管理器，请键入*Verifer*在命令提示符。 可以配置你想要验证的驱动程序。 验证驱动程序的代码将添加开销在运行，因此请尝试并验证尽可能最少数量的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。


**时间的差旅跟踪**

如果可以按要求重现 bug 检查，调查花些时间旅行跟踪使用 WinDbg 预览的可能性。 有关详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。

