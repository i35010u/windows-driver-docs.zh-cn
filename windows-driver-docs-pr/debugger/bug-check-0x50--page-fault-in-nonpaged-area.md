---
title: Bug 检查 0x50 PAGE_FAULT_IN_NONPAGED_AREA
description: PAGE_FAULT_IN_NONPAGED_AREA bug 检查的值为 0x00000050。 这表明引用了无效的系统内存。
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
ms.localizationpriority: high
ms.openlocfilehash: 422a1d261f72506bfba0149a0af9620e55a3a249
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252853"
---
# <a name="bug-check-0x50-page_fault_in_nonpaged_area"></a>Bug 检查 0x50：PAGE\_FAULT\_IN\_NONPAGED\_AREA


PAGE\_FAULT\_IN\_NONPAGED\_AREA bug 检查的值为 0x00000050。 这表明引用了无效的系统内存。 通常，内存地址错误或内存地址指向已释放的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="page_fault_in_nonpaged_area-parameters"></a>PAGE\_FAULT\_IN\_NONPAGED\_AREA 参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
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
<p><i>Windows 1507 (TH1) 版本 - x64 后</i> </p>
<p><strong>0:</strong>读取操作</p>
<p><strong>2:</strong>写入操作</p>
<p><strong>10:</strong>执行操作</p>

<p><i>Windows 1507 (TH1) 版本 - x86 后</i></p>
<p><strong>0:</strong>读取操作</p>
<p><strong>2:</strong>写入操作</p>
<p><strong>10:</strong>执行操作</p>

<p><i>Windows 1507 (TH1) 版本 - ARM 后</i></p>
<p><strong>0:</strong>读取操作</p>
<p><strong>1:</strong>写入操作</p>
<p><strong>8:</strong>执行操作</p>

<p><i>Windows 1507 (TH1) 版本 x64 / x86 前</i></p>
<p><strong>0:</strong>读取操作</p>
<p><strong>1:</strong>写入操作</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>引用内存的地址（如果已知）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>页面错误类型</p>
<p>0x03-NONPAGED_BUGCHECK_WRONG_SESSION - 尝试在没有会话的进程的上下文中引用会话空间地址。  通常，这意味着调用方在未首先正确获取对正确进程的对象引用并附加到该进程的情况下，不正确地尝试访问会话地址。 此 bug 检查和子类型最后用于 Windows 10 RS3 中。  在 Windows 10 RS4 及更高版本中，此错误改为 0x02 (NONPAGED_BUGCHECK_NOT_PRESENT_PAGE_TABLE)。</p>
<p>NONPAGED_BUGCHECK_VA_NOT_CANONICAL 0x04 - 尝试引用非规范（非法）虚拟地址（参数 1）。  调用方不会尝试访问此地址。</p>
</td>
</tr>
</tbody>
</table>

 
如果能够识别出导致错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的 (PUNICODE\_STRING) KiBugCheckDriver  位置。 可以使用以下调试程序 dx 命令来显示它 - `dx KiBugCheckDriver`。

<a name="cause"></a>原因
-----

安装了错误的系统服务或错误的驱动程序代码都可能造成 Bug 检查 0x50。 防病毒软件和损坏的 NTFS 卷也可能触发此错误。

安装有故障的硬件之后，或者安装的硬件出现故障时（通常与 RAM 缺陷有关，包括主存储器、二级 RAM 缓存或视频 RAM 缺陷），也可能出现此错误。


<a name="remarks"></a>备注
----------

**事件日志：** 检查事件查看器中的系统日志，以获取可能有助于查明导致错误的设备或驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 在系统日志中查找与蓝屏同时出现的严重错误。

**解决驱动程序问题：** 如果驱动程序的名称在蓝屏上列出或出现在事件日志中，请检查该名称。 请与驱动程序供应商联系，查看是否有更新的驱动程序可用。 

**解决系统服务故障问题：** 禁用服务并确认此操作是否可解决错误。 如果可以，请联系系统服务的制造商以了解可能的更新。 如果在系统启动期间发生错误，请调查 Windows 修复选项。 有关详细信息，请参阅 [Windows 10 中的恢复选项](https://support.microsoft.com/help/12415/windows-10-recovery-options)。

**解决防病毒软件问题：** 禁用程序并确认此操作是否解决了错误。 如果是，请与程序制造商联系，了解可能的更新。

**解决损坏的 NTFS 卷问题：** 运行“Chkdsk/f/r”来检测和修复磁盘错误  。 在系统分区上开始磁盘扫描之前，必须重启系统。 请与硬盘驱动器系统制造商联系，找到他们为硬盘驱动子系统提供的任何诊断工具。

**Windows 内存诊断：** 运行 Windows 内存诊断工具，测试物理内存。 选择“开始”按钮，再选择“控制面板”。 在搜索框中，键入“内存”，然后选择“诊断计算机的内存问题”。运行测试后，使用事件查看器在系统日志下查看结果。 查找“内存诊断结果”条目以查看结果  。

**解决硬件问题：** 如果最近在系统中添加了硬件，请将其删除以查看错误是否再次出现。 如果现有硬件出现故障，请卸下或更换故障部件。 你应运行系统制造商提供的硬件诊断。 有关这些过程的详细信息，请参阅计算机的用户手册。

有关一般蓝屏疑难解答信息，请参阅[蓝屏数据](blue-screen-data.md)  。

<a name="resolution"></a>解决方法
----------

通常，引用的地址在释放的内存中，或者是无效的。 这不能通过“try-except”处理程序保护，只能由探测或类似的编程技术保护  。

通过 -v 详细选项使用 [!analyze](-analyze.md) 调试扩展，以显示有关错误检查的信息，从而确定根本原因  。

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

在本例中，参数 2 表示在读取内存区域时发生 bug 检查。

查看所有 !analyze 输出，以了解进行 bug 检查时发生的情况。 检查 MODULE_NAME: 和 FAULTING_MODULE: 以查看引用无效系统内存涉及的代码。

请查看“堆栈文本”以获取故障发生时运行的内容的线索。 如果有多个转储文件可用，请比较信息以查找堆栈中的通用代码。

使用 !analyze 输出中提供的 .trap 命令以设置上下文。

```dbgcmd
TRAP_FRAME:  fffff98112e8b3d0 -- (.trap 0xfffff98112e8b3d0)
```

 使用调试器命令，例如使用 [kb（显示堆栈回溯）](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)来调查错误代码  。

使用 `lm t n` 列出内存中加载的模块。

使用 [d、da、db、dc、dd、dD、df、dp、dq、du、dw（显示内存）](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令调查参数 1 和参数 3 引用的内存区域。

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
在本例中，参数 1 中的内存区域中似乎没有数据，该参数是试图读取的内存区域。

使用 [!address](-address.md) 命令查看参数 3，该参数是引用错误内存的指令的地址。

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

使用参数 3 的 [u、ub、uu（取消汇编）反汇编](u--unassemble-.md)检查引用错误内存的对象。 有关 X64 处理器和汇编语言的详细信息，请参阅 [X64 处理器](the-x64-processor.md)。 

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

使用 `ub` 从给定地址向后分解。

使用 [r（寄存器）](r--registers-.md)命令检查在检查系统 bug 时执行的操作。 

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

在这种情况下，`fffff80240d322f9` 位于指令指针寄存器 rip 中。

`!pte` 和 `!pool` 命令也可用于检查内存。

使用 `!memusage` 检查系统内存的一般状态。 

**驱动程序验证程序**

驱动程序验证程序是一个实时运行的工具，用于检查驱动程序的行为。 例如，驱动程序验证程序检查内存资源（如内存池）的使用。 如果在执行驱动程序代码时发现错误，它会主动创建一个异常，以允许进一步检查该部分驱动程序代码。 驱动程序验证程序管理器内置于 Windows 中，可在所有 Windows PC 上使用。 若要启动驱动程序验证程序管理器，请在命令提示下键入“验证程序”  。 你可以配置要验证的驱动程序。 验证驱动程序的代码在运行时会增加开销，因此请尝试验证尽可能少的驱动程序。 有关详细信息，请参阅[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。

