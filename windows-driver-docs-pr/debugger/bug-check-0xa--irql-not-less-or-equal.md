---
title: Bug 检查 0xA 对 IRQL_NOT_LESS_OR_EQUAL
description: 对 IRQL_NOT_LESS_OR_EQUAL bug 检查具有 0x0000000A 值。
ms.assetid: a32b80f5-9822-41af-8668-836a70b05c0f
keywords:
- Bug 检查 0xA 对 IRQL_NOT_LESS_OR_EQUAL
- IRQL_NOT_LESS_OR_EQUAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22145baa0432ad4af7b7744c54d4f9c6aa8b4de8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367251"
---
# <a name="bug-check-0xa-irqlnotlessorequal"></a>Bug 检查 0xA：IRQL\_NOT\_LESS\_OR\_EQUAL


IRQL\_不\_较少\_或\_相等 bug 检查的值为 0x0000000A。 这表示 Microsoft Windows 或访问的内核模式驱动程序都分页内存地址无效时引发的中断请求级别 (IRQL)。 这通常是错误的指针或 pageability 问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="irqlnotlessorequal-parameters"></a>IRQL\_不\_较少\_或\_等于参数


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
<td align="left"><p>无法访问虚拟内存地址。</p>
<p>使用 <strong><a href="-pool.md" data-raw-source="[!pool](-pool.md)">！ 池</a></strong>上此地址来查看它是否是分页的池。 这些命令，也可能收集有关失败的信息很有用：  <strong><a href="-pte.md" data-raw-source="[!pte](-pte.md)">！ pte</a></strong>，  <strong><a href="-address.md" data-raw-source="[!address](-address.md)">！ 地址</a></strong>，和<strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln （列出最近的符号）</a></strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL 在错误的时间。</p>
<p>值：</p>
<p>2 :IRQL DISPATCH_LEVEL 时所处的错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>描述导致错误的操作的位域。</p>
<p><strong>位 0:</strong></p>
<p>值：</p>
<p>0:读取操作</p>
<p>1：写入操作</p>
<p><strong>位 3:</strong>（仅适用于支持此级别的报告的芯片集。）</p>
<p>值：</p>
<p>0:不是执行的操作</p>
<p>1：执行操作</p>
<strong>位 0 并结合使用的位 3 值：</strong>
<p>0x0:尝试读取发件人地址在参数 1 中的错误。</p>
<p>0x1:尝试写入到的地址在参数 1 中的错误。</p>
<p>0x8:尝试从参数 1 中的地址执行代码的错误。</p>
<p>此值通常引起:</p>
<ul>
<li>调用的函数不能在 DISPATCH_LEVEL 在 DISPATCH_LEVEL 时调用</li>
<li>忘记释放自旋锁</li>
<li>标记为可分页的代码，但必须为非可分页 （例如，因为代码获取调节锁，或在 DPC 中调用）</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>指令指针时的错误。</p>
<p>使用<strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln （列表最接近符号）</a></strong>命令此地址来查看函数的名称。</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

Bug 检查 0xA 通常被由于内核模式设备驱动程序使用不正确的地址。

检查此错误表示尝试访问无效的地址处引发的中断请求级别 (IRQL)。 这是错误的内存指针或设备驱动程序代码有 pageability 问题。

以下是可以使用一些通用准则 catergorize 到类型的编码错误 tha 导致 bug 检查。

- 如果参数 1 为小于 0x1000 控制，这很可能为 NULL 指针取消引用。

- 如果[！ 池](-pool.md)参数 1 为分页池 （或其他类型的可分页内存），则 IRQL 是过大，无法访问此数据的报表。 在较低的 IRQL 运行，或者分配的非分页池中的数据。

- 如果参数 3 指示这是尝试执行可分页的代码，则 IRQL 是过大，无法调用此函数。 在较低的 IRQL 运行或未标记为可分页的代码。

- 否则，这可能是错误的指针，可能是因为使用后释放或位翻转。 调查使用的参数 1 的有效性[ **！ pte**](-pte.md)， [ **！ 地址**](-address.md)，并[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)。


<a name="resolution"></a>分辨率
----------

如果可用的内核调试程序，获取堆栈跟踪： [ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示 bug 检查有关的信息并可有助于确定根本原因，然后输入之一[**k （显示堆栈回溯）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)命令以查看调用堆栈。

**收集的信息**

如果在蓝色屏幕上的已列出，请检查驱动程序的名称。

检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

**驱动程序验证程序**

驱动程序验证程序是一种工具，运行实时检查驱动程序的行为。 例如，驱动程序验证工具将检查内存资源，如内存池的使用。 如果它发现错误的驱动程序代码执行过程中，它会主动创建例外以允许驱动程序代码以进行进一步仔细检查该部分。 驱动程序验证程序管理器内置于 Windows，可在所有 Windows Pc 上。 若要启动驱动程序验证程序管理器，请键入*Verifer*在命令提示符。 可以配置你想要验证的驱动程序。 验证驱动程序的代码将添加开销在运行，因此请尝试并验证尽可能最少数量的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。

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

有故障的设备驱动程序、 系统服务或 BIOS 的安装后发生此错误通常生成此 bug 检查。

如果遇到 bug 检查 0xA 升级到更高版本的 Windows 时，可能会通过设备驱动程序、 系统服务、 病毒扫描程序或与新的版本不兼容的备份工具导致此错误。

**解决硬件故障问题：** 如果硬件具有最近添加到系统，则删除它才能看到如果错误重复出现。 如果现有硬件出现故障，删除或更换有故障的组件。 应运行硬件诊断系统制造商提供。 有关这些过程的详细信息，请参阅您的计算机的所有者的手册。

**解决错误系统服务问题：** 禁用服务，并确认这会解决该错误。 如果是这样，请与系统服务有关的可能更新的制造商联系。 如果在系统启动期间发生错误，请调查 Windows 修复选项。 有关详细信息，请参阅[Windows 10 中的恢复选项](https://support.microsoft.com/help/12415/windows-10-recovery-options)。

**在解决有关防病毒软件问题：** 禁用计划，并确认这会解决该错误。 如果是这样，请与联系有关可能的更新程序的制造商。

有关常规的蓝色屏幕上，故障排除信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。
