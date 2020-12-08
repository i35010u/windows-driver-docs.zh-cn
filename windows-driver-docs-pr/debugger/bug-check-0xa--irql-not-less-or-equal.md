---
title: Bug 检查 0xA IRQL_NOT_LESS_OR_EQUAL
description: IRQL_NOT_LESS_OR_EQUAL bug 检查的值为0x0000000A。
keywords:
- Bug 检查 0xA IRQL_NOT_LESS_OR_EQUAL
- IRQL_NOT_LESS_OR_EQUAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe86cdf4f6904eb0323bb745bb382783cf0d596a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804305"
---
# <a name="bug-check-0xa-irql_not_less_or_equal"></a>Bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于


IRQL \_ 不 \_ 小于 \_ 或 \_ 等于 bug 检查的值为0x0000000a。 这表明 Microsoft Windows 或内核模式驱动程序以无效的地址访问分页内存，而在中断请求级别 (IRQL) 。 这通常是错误指针或 pageability 问题的结果。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="irql_not_less_or_equal-parameters"></a>IRQL \_ 不 \_ 小于 \_ 或 \_ 等于参数


<table>
<colgroup>
<col width="20%" />
<col width="80%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td align="left"><p>无法访问的虚拟内存地址。</p>
<p>使用此地址上的 <strong><a href="-pool.md" data-raw-source="[!pool](-pool.md)">！池</a></strong> 来查看其是否已分页。 这些命令在收集有关失败的信息时，可能也很有用： <strong><a href="-pte.md" data-raw-source="[!pte](-pte.md)">！ pte</a></strong>， <strong><a href="-address.md" data-raw-source="[!address](-address.md)">！ address</a></strong>， <strong> <a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln </strong> (列出最近的符号) </a>。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td align="left"><p>出现故障时的 IRQL。</p>
<p>分隔</p>
<ul><li><p><strong>2</strong>：错误时 DISPATCH_LEVEL IRQL。</p></li></ul></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td align="left"><p>描述导致错误的操作的位域。 请注意，bit 3 仅在支持此级别的报告的芯片组上可用。</p>
<p><strong>位0值：</strong></p>
<ul><li><p>0-读取操作</p></li>
<li><p>1-写入操作</p></li></ul>
<p><strong>第3位值：</strong></p>
<ul>
<li><p>0-不是执行操作</p></li>
<li><p>1-执行操作</p></li>
</ul>
<p><strong>位0和位3组合值：</strong></p>
<ul>
<li><p>0x0-尝试从参数1中的地址读取时出错。</p></li>
<li><p>0x1-尝试写入参数1中的地址时出错。</p></li>
<li><p>0x8-尝试从参数1中的地址执行代码时出错。</p></li>
</ul>
<p>此值通常由以下原因引起：</p>
<ul>
<li>调用在 DISPATCH_LEVEL 时无法在 DISPATCH_LEVEL 调用的函数。</li>
<li>忘记发布旋转锁。</li>
<li>如果代码必须不可分页，则将代码标记为可分页 (例如，因为代码获取旋转锁，或在延迟的过程调用) 中调用。</li>
</ul>
</td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td align="left"><p>出现错误时的指令指针。</p>
<p>使用 <strong> <a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln (列出此地址上的 </strong> 最接近符号) </a>命令可查看函数的名称。</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

此 bug 检查通常是由于使用了不正确地址的内核模式设备驱动程序导致的。

此 bug 检查表明尝试访问无效的地址，同时在中断请求级别 (IRQL) 。 这是错误的内存指针或设备驱动程序代码的 pageability 问题。

下面是一些一般准则，可用于对导致 bug 检查的编码错误类型进行分类：

- 如果参数1小于0x1000，则问题可能是 NULL 指针取消引用。

- 如果 [**！池**](-pool.md) 报告参数1为分页池 (或其他类型的可分页内存) ，则 IRQL 太高，无法访问此数据。 以较低的 IRQL 运行，或分配非分页池中的数据。

- 如果参数3指示此尝试执行可分页的代码，则 IRQL 太高，无法调用此函数。 以较低的 IRQL 运行，或者不将代码标记为可分页。

- 否则，这可能是一个错误指针，可能是由于使用不到或进行反向。 调查参数1的有效性，其中包含 [**！ pte**](-pte.md)， [**！ address**](-address.md)和 [ **ln** (列出最近的符号)](ln--list-nearest-symbols-.md)。


<a name="resolution"></a>解决方法
----------

如果内核调试器可用，则获取堆栈跟踪。 首先运行 [**！分析**](-analyze.md) 调试器扩展，以显示有关 bug 检查的信息。  (**！分析** 扩展可帮助确定根本原因。 ) 接下来，输入一个 [ * *k \** _ (显示 stack backtrace)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令以查看调用堆栈。

### <a name="gather-information"></a>收集信息

检查在蓝屏上列出的驱动程序的名称。

检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 在系统日志中查找与蓝屏同时出现的严重错误。

### <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证程序是一个实时运行的工具，用于检查驱动程序的行为。 例如，驱动程序验证程序检查内存资源（如内存池）的使用。 如果它标识了驱动程序代码执行过程中的错误，它会主动创建一个例外，以允许进一步审查驱动程序代码的一部分。 驱动程序验证程序管理器内置于 Windows 中，在所有 Windows Pc 上都可用。 

若要启动驱动程序验证程序管理器，请在命令提示符下键入 _ *Verifier**。 你可以配置要验证的驱动程序。 验证驱动程序的代码会在运行时增加开销，因此请尝试尽可能多地验证驱动程序。 有关详细信息，请参阅[驱动程序验证程序](../devtest/driver-verifier.md)。

下面是一个调试示例：

```dbgcmd
kd> .bugcheck       [Lists bug check data.]
Bugcheck code 0000000a
Arguments 00000000 0000001c 00000000 00000000

kd> kb [Lists the stack trace.]
ChildEBP RetAddr  Args to Child
8013ed5c 801263ba 00000000 00000000 e12ab000 NT!_DbgBreakPoint
8013eecc 801389ee 0000000a 00000000 0000001c NT!_KeBugCheckEx+0x194
8013eecc 00000000 0000000a 00000000 0000001c NT!_KiTrap0E+0x256
8013ed5c 801263ba 00000000 00000000 e12ab000
8013ef64 00000246 fe551aa1 ff690268 00000002 NT!_KeBugCheckEx+0x194

kd> kv [Lists the trap frames.]
ChildEBP RetAddr  Args to Child
8013ed5c 801263ba 00000000 00000000 e12ab000 NT!_DbgBreakPoint (FPO: [0,0,0])
8013eecc 801389ee 0000000a 00000000 0000001c NT!_KeBugCheckEx+0x194
8013eecc 00000000 0000000a 00000000 0000001c NT!_KiTrap0E+0x256 (FPO: [0,0] TrapFrame @ 8013eee8)
8013ed5c 801263ba 00000000 00000000 e12ab000
8013ef64 00000246 fe551aa1 ff690268 00000002 NT!_KeBugCheckEx+0x194

kd> .trap 8013eee8 [Gets the registers for the trap frame at the time of the fault.]
eax=dec80201 ebx=ffdff420 ecx=8013c71c edx=000003f8 esi=00000000 edi=87038e10
eip=00000000 esp=8013ef5c ebp=8013ef64 iopl=0         nv up ei pl nz na pe nc
cs=0008  ss=0010  ds=0023  es=0023  fs=0030  gs=0000             efl=00010202
ErrCode = 00000000
00000000 ???????????????    [The current instruction pointer is NULL.]

kd> kb       [Gives the stack trace before the fault.]
ChildEBP RetAddr  Args to Child
8013ef68 fe551aa1 ff690268 00000002 fe5620d2 NT!_DbgBreakPoint
8013ef74 fe5620d2 fe5620da ff690268 80404690
NDIS!_EthFilterIndicateReceiveComplete+0x31
8013ef64 00000246 fe551aa1 ff690268 00000002 elnkii!_ElnkiiRcvInterruptDpc+0x1d0
```

<a name="remarks"></a>备注
-------

生成此 bug 检查的错误通常在安装了有故障的设备驱动程序、系统服务或 BIOS 之后发生。

如果在升级到较新版本的 Windows 时遇到 bug 检查0xA，则该错误可能是由于设备驱动程序、系统服务、病毒扫描程序或与新版本不兼容的备份工具导致的。

**解决硬件问题：** 如果最近在系统中添加了硬件，请将其删除以查看错误是否再次出现。 如果现有硬件出现故障，请卸下或更换故障部件。 运行系统制造商提供的硬件诊断。 有关这些过程的详细信息，请参阅计算机的用户手册。

**解决故障系统服务问题：** 禁用服务并确认是否可以解决此错误。 如果可以，请联系系统服务的制造商以了解可能的更新。 如果在系统启动期间发生错误，请调查 Windows 修复选项。 有关详细信息，请参阅 [Windows 10 中的恢复选项](https://support.microsoft.com/help/12415/windows-10-recovery-options)。

**解决防病毒软件问题：** 禁用该程序并确认是否解析此错误。 如果是，请与程序制造商联系，了解可能的更新。

有关解决 bug 检查问题的常规信息，请参阅 [蓝色屏幕数据](blue-screen-data.md)。
