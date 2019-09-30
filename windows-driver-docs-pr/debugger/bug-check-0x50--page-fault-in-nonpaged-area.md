---
title: Bug 检查 0x50 PAGE_FAULT_IN_NONPAGED_AREA
description: PAGE_FAULT_IN_NONPAGED_AREA bug 检查的值为0x00000050。 这表明引用了无效的系统内存。
ms.assetid: 63b4ab82-f7a9-4e14-bf7c-707a22d7e251
keywords:
- Bug 检查 0x50 PAGE_FAULT_IN_NONPAGED_AREA
- PAGE_FAULT_IN_NONPAGED_AREA
ms.date: 04/18/2019
topic_type:
- apiref
api_name:
- PAGE_FAULT_IN_NONPAGED_AREA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b046ff169db86578684c12ae37f4c8b106e18dba
ms.sourcegitcommit: 667b4be765b2eac6bc586d39abef3393a718b23f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2019
ms.locfileid: "70025326"
---
# <a name="bug-check-0x50-page_fault_in_nonpaged_area"></a>Bug 检查 0x50：PAGE @ NO__T-0FAULT @ NO__T-1IN @ NO__T-2NONPAGED @ NO__T-3AREA


页面 @ no__t-0FAULT @ no__t-1IN @ no__t-2NONPAGED @ no__t-3AREA bug 检查的值为0x00000050。 这表明引用了无效的系统内存。 通常，内存地址错误或内存地址指向已释放的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户, 请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="page_fault_in_nonpaged_area-parameters"></a>PAGE @ no__t-0FAULT @ no__t-1IN @ no__t-2NONPAGED @ no__t-3AREA 参数


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
<td align="left">
<p><i>Windows 1507 （TH1）版本之后-x64 </i> </p>
<p><strong>0</strong>读取操作</p>
<p><strong>2：10</strong>写入操作</p>
<p><strong>万</strong>执行操作</p>

<p><i>Windows 1507 （TH1）版本-x86 之后</i></p>
<p><strong>0</strong>读取操作</p>
<p><strong>2：10</strong>写入操作</p>
<p><strong>万</strong>执行操作</p>

<p><i>Windows 1507 （TH1）版本-ARM 之后</i></p>
<p><strong>0</strong>读取操作</p>
<p><strong>2</strong>写入操作</p>
<p><strong>8</strong>执行操作</p>

<p><i>在 Windows 1507 （TH1）版本 x64/x86 之前</i></p>
<p><strong>0</strong>读取操作</p>
<p><strong>2</strong>写入操作</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>确定所引用内存的地址（如果已知）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>页错误类型</p>
<p>0x03-NONPAGED_BUGCHECK_WRONG_SESSION-尝试引用会话空间地址在没有会话的进程上下文中进行。  通常，这意味着调用方不会正确地尝试访问会话地址，而无需正确获取到正确进程的对象引用并首先附加到该地址。 此错误检查 & 子类型上次在 Windows 10 RS3 中使用。  在 Windows 10 RS4 及更高版本中，此错误改为显示为0x02 （NONPAGED_BUGCHECK_NOT_PRESENT_PAGE_TABLE）。</p>
<p>0x04-NONPAGED_BUGCHECK_VA_NOT_CANONICAL-尝试引用非规范（非法）虚拟地址（参数1）。  调用方决不会尝试访问此地址。</p>
</td>
</tr>
</tbody>
</table>

 
如果可以识别负责错误的驱动程序，其名称将打印在蓝色屏幕上，并存储在内存中的位置（PUNICODE @ no__t-0STRING） **KiBugCheckDriver**。 可以使用调试程序 dx 命令显示此 `dx KiBugCheckDriver`。

<a name="cause"></a>原因
-----

Bug 检查0x50 可能是由于安装了故障系统服务或错误的驱动程序代码引起的。 防病毒软件还可以触发此错误，这也会导致 NTFS 卷损坏。

在安装有故障的硬件或发生故障时，还可能会发生此问题（通常与有缺陷的 RAM 相关，是主内存、L2 RAM 缓存或视频 RAM）。


<a name="remarks"></a>备注
----------

**事件日志：** 检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 有关详细信息，请参阅[Open 事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 在与蓝色屏幕相同的时间范围内查找系统日志中的严重错误。

**解决驱动程序问题：** 如果驱动程序的名称列在蓝色屏幕上或出现在事件日志中，请检查该驱动程序的名称。 请与驱动程序供应商联系，以查看是否有更新的驱动程序可用。 

**解决故障系统服务问题：** 禁用服务并确认此错误是否解决。 如果是这样，请与系统服务制造商联系，了解可能的更新。 如果在系统启动过程中出现错误，则调查 Windows 修复选项。 有关详细信息，请参阅[Windows 10 中的恢复选项](https://support.microsoft.com/help/12415/windows-10-recovery-options)。

**解决防病毒软件问题：** 禁用程序并确认此错误是否解决。 如果是这样，请与程序的制造商联系，了解可能的更新。

**解决 NTFS 卷损坏问题：** 运行**Chkdsk/f/r**以检测和修复磁盘错误。 在磁盘扫描开始之前，必须重新启动系统。 请联系硬驱动程序系统的制造商，查找他们为硬盘驱动器子系统提供的任何诊断工具。

**Windows 内存诊断：** 运行 Windows 内存诊断工具来测试物理内存。 单击 "开始" 按钮，然后单击 "控制面板"。 在搜索框中，键入 "内存"，然后单击 "*诊断计算机的内存问题*"。运行测试后，使用事件查看器查看系统日志下的结果。 查找 " *MemoryDiagnostics* " 项，查看结果。

**解决硬件问题：** 如果最近将硬件添加到系统中，请将其删除，查看错误是否重复出现。 如果现有硬件出现故障，请删除或替换故障组件。 你应运行系统制造商提供的硬件诊断。 有关这些过程的详细信息，请参阅计算机所有者手册。

有关一般的蓝屏疑难解答信息，请参阅[**蓝屏数据**](blue-screen-data.md)。

<a name="resolution"></a>分辨率
----------

通常，引用的地址在释放的内存中，或者只是无效的。 这不能通过**try-except**处理程序进行保护，只可通过探测或类似的编程技术来保护它。

使用 "使用-v verbose[**分析**](-analyze.md)调试扩展" 选项可显示有关 bug 检查的信息，以确定问题的根本原因。

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

在此示例中，参数2指示在读取内存区域时发生 bug 检查。

查看所有！分析输出，以获取有关 bug 检查发生时正在进行的操作的信息。 检查 MODULE_NAME：和 FAULTING_MODULE：以查看引用无效系统内存时涉及哪些代码。

查看堆栈文本，以获取发生故障时正在运行的内容的线索。 如果有多个转储文件可用，则比较信息以查找堆栈中的通用代码。

使用在！分析输出中提供的 trap 命令来设置上下文。

```dbgcmd
TRAP_FRAME:  fffff98112e8b3d0 -- (.trap 0xfffff98112e8b3d0)
```

 使用诸如使用[**kb （显示 Stack Backtrace）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)之类的调试器命令调查错误代码。

使用 `lm t n` 列出在内存中加载的模块。

使用[d，da，db，dc，dd，dd，df，dp，dq，du，dw （显示内存）](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令调查参数1和参数3引用的内存区域。

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
在这种情况下，此内存区域中的数据可能不在参数1中，这是尝试读取的内存区域。

使用[！ address](-address.md)命令查看参数3，它是引用错误内存的指令的地址。

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

使用[u，ub，uu （Unassemble） Dissasemble](u--unassemble-.md)与参数3来检查引用了错误内存的。 有关 X64 处理器和汇编语言的详细信息，请参阅[X64 处理器](the-x64-processor.md)。 

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

使用 `ub` 从给定地址向后 dissassemble。

使用[r （寄存器）](r--registers-.md)命令检查在检查系统错误时执行的操作。 

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

在这种情况下 `fffff80240d322f9` 位于指令指针 register，即 rip 中。

@No__t （0）和 @no__t 1 命令也可用于检查内存。

使用 @no__t 和来检查系统内存的一般状态。 

**驱动程序验证程序**

驱动程序验证程序是一种实时运行的工具，用于检查驱动程序的行为。 例如，驱动程序验证程序检查内存资源的使用情况，例如内存池。 如果发现驱动程序代码执行过程中出现错误，它会主动创建一个例外，以允许进一步审查驱动程序代码的一部分。 驱动程序验证器管理器内置于 Windows 中，在所有 Windows Pc 上都可用。 若要启动驱动程序验证器管理器，请在命令提示符处键入*Verifer* 。 你可以配置要验证的驱动程序。 验证驱动程序的代码会在运行时增加开销，因此请尝试并尽可能多地验证驱动程序。 有关详细信息，请参阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。

