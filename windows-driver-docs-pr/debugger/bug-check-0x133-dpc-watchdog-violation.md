---
title: Bug 检查 0x133 DPC_WATCHDOG_VIOLATION
description: DPC_WATCHDOG_VIOLATION bug 检查的值为0x00000133。
keywords:
- Bug 检查 0x133 DPC_WATCHDOG_VIOLATION
- DPC_WATCHDOG_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DPC_WATCHDOG_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 096740ddc90d3416a2085ea2b615c07552ff22e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802023"
---
# <a name="bug-check-0x133-dpc_watchdog_violation"></a>Bug 检查 0x133 DPC \_ 监视程序 \_ 冲突


DPC \_ 监视程序 \_ 冲突 bug 检查的值为0x00000133。 此 bug 检查指示已执行 DPC 监视程序，原因是它检测到 (DPC) 的单个长时间运行的延迟过程调用，或者系统在中断请求级别花费了长时间， (IRQL) \_ 或更高级别。 参数1的值指示单个 DPC 是否超出了超时，或者系统是否累积了很长一段时间，以 IRQL 调度 \_ 级别或更高级别。 Dpc 的运行时间不应超过100微秒，并且 Isr 的运行时间不应超过25微秒，但系统上的实际超时值设置得更高。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="dpc_watchdog_violation-parameters"></a>DPC \_ 监视程序 \_ 冲突参数


*参数 1* 指示违规类型。 其他参数的意义取决于 *参数 1* 的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>DPC 时间计数 (以刻度) </p></td>
<td align="left"><p>DPC 时间配额 (以计时) 为单位。</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>单个 DPC 或 ISR 超出了其时间配额。 通常可以使用堆栈跟踪标识有问题的组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>监视周期</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>系统累积 DISPATCH_LEVEL 或更高版本上的时间较长的一段时间。 通常可以使用堆栈跟踪标识有问题的组件。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

**参数 1 = 0**

在此示例中，时钟周期计数为501，超过 DPC 时间为500。 映像名称指示在 bug 检查发生时执行此代码。

```dbgcmd
0: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

DPC_WATCHDOG_VIOLATION (133)
The DPC watchdog detected a prolonged run time at an IRQL of DISPATCH_LEVEL
or above.
Arguments:
Arg1: 0000000000000000, A single DPC or ISR exceeded its time allotment. The offending
    component can usually be identified with a stack trace.
Arg2: 0000000000000501, The DPC time count (in ticks).
Arg3: 0000000000000500, The DPC time allotment (in ticks).
Arg4: 0000000000000000

...

IMAGE_NAME:  BthA2DP.sys
...
```

使用以下调试器命令收集有关参数为0的失败的详细信息：

[**k (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) ，以查看发生停止代码时运行的代码。

你可能想要使用 u、ub、uu (Unassemble) 命令，更深入地了解正在运行的代码的详细信息。

[**！ Pcr**](-pcr.md)扩展显示特定处理器 (pcr) 的处理器控制区域的当前状态。 在中，输出将为 Prcb 的地址。

```dbgcmd
                     Prcb: fffff80309974180
```

可以使用 [**dt (显示类型)**](dt--display-type-.md) 命令显示有关 DPC 和 dpc 监视程序的其他信息。 对于该地址，请使用！ pcr 输出中列出的 Prcb：

```dbgcmd
dt nt!_KPRCB fffff80309974180 Dpc* 
```

**参数 1 = 1**

对于参数1，代码可能不会在有问题的代码区域中停止。 在这种情况下，一种方法是使用事件跟踪来尝试跟踪哪个驱动程序的执行持续时间超过了其正常执行时间。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用！分析扩展](using-the--analyze-extension.md) 和 [！分析](-analyze.md)

<a name="remarks"></a>备注
-------

通常，此 stop 代码是由在特定情况下出现故障的驱动程序代码引起的，不会在分配的时间范围内完成其工作。

如果你不具备使用 Windows 调试器来解决此问题，则应使用一些基本的故障排除方法。

-   如果在 bug 检查消息中标识了驱动程序，则若要隔离此问题，请禁用该驱动程序。 咨询制造商以获取驱动程序更新。

-   检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于识别导致 bug 检查0x133 的设备或驱动程序。

-   确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在 [Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

-   有关其他常规疑难解答信息，请参阅 [**蓝屏数据**](blue-screen-data.md)。

 

 




