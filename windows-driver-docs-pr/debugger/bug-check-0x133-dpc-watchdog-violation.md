---
title: Bug 检查 0x133 DPC_WATCHDOG_VIOLATION
description: DPC_WATCHDOG_VIOLATION bug 检查具有 0x00000133 值。
ms.assetid: CE9A4CBF-0016-42F7-A9EE-56DF6E61593A
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
ms.openlocfilehash: f780d210c5d337f02cf017c9e7c68a3d854c82fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351247"
---
# <a name="bug-check-0x133-dpcwatchdogviolation"></a>Bug 检查 0x133 DPC\_监视器\_冲突


DPC\_监视器\_冲突错误检查的值为 0x00000133。 此 bug 检查指示 DPC 监视程序执行，因为它检测到的单个运行时间较长延迟的过程调用 (DPC) 或系统在中断请求级别 (IRQL) 花费很长时间的时间的调度\_级别或更高版本。 参数 1 的值指示单个 DPC 是否超出了超时或系统是否累积所用的 IRQL 调度时间长\_级别或更高版本。 Dpc 不应运行时间超过 100 微秒和 Isr 不应运行时间超过 25 微秒为单位，但是将实际超时值在系统上设置高得多。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="dpcwatchdogviolation-parameters"></a>DPC\_监视器\_冲突参数


*参数 1*指示冲突类型。 其他参数的含义取决于的值*参数 1*。

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
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>DPC 时间计数 （以刻度为单位）</p></td>
<td align="left"><p>DPC 时间的配额 （以刻度为单位）。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>单个 DPC 或 ISR 超出其时间服务配额。 通常可以使用堆栈跟踪标识有问题的组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>监视程序段</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>系统累积所用 IRQL DISPATCH_LEVEL 或更高的时间长的的时间。 通常可以使用堆栈跟踪标识有问题的组件。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

**参数 1 = 0**

在此示例中，501 的时钟周期数超过 500 的 DPC 时间分配。 映像名称指示 bug 检查发生时正在执行此代码。

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

使用以下调试器命令收集失败，参数为 0 的详细信息：

[**k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)若要查看哪些代码停止代码发生时正在运行。

要使用 u、 ub、 uu （反汇编） 命令以查看更深层次细节的正在运行的代码。

[ **！ Pcr** ](-pcr.md)扩展特定处理器上显示的当前状态的处理器控件区域 (PCR)。 在输出中将 Prcb 的地址

```dbgcmd
                     Prcb: fffff80309974180
```

可以使用[ **dt （显示类型）** ](dt--display-type-.md)命令以显示有关 Dpc 和 DPC 监视程序的其他信息。 对于地址，使用列入 Prcb ！ pcr 输出：

```dbgcmd
dt nt!_KPRCB fffff80309974180 Dpc* 
```

**参数 1 = 1**

对于为 1 的参数，该代码可能不会停止的代码有问题的区域中。 在这种情况下一种方法是使用事件跟踪来尝试跟踪哪些驱动程序而不它的正常执行持续时间。

有关详细信息，请参阅以下主题：

[故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md)

[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用 ！ 分析扩展](using-the--analyze-extension.md)和[！ 分析](-analyze.md)

<a name="remarks"></a>备注
-------

一般情况下此停止代码是由错误的驱动程序代码引起的某些情况下，不会完成其工作分配的时间范围内。

如果您未配有使用 Windows 调试器到此问题，则应使用一些基本的故障排除方法。

-   如果 bug 检查消息中标识一个驱动程序，则若要隔离此问题，禁用驱动程序。 请咨询制造商，驱动程序更新。

-   有关其他错误消息可能有助于识别设备或驱动程序导致 bug 检查 0x133 检查事件查看器中的系统日志。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

 

 




