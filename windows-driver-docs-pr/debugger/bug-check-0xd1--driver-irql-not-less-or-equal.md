---
title: Bug 检查 0xD1 DRIVER_IRQL_NOT_LESS_OR_EQUAL
description: DRIVER_IRQL_NOT_LESS_OR_EQUAL bug 检查的值为0x000000D1。 这表示内核模式驱动程序试图在进程 IRQL 上访问分页内存过高的情况。
keywords:
- Bug 检查 0xD1 DRIVER_IRQL_NOT_LESS_OR_EQUAL
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
ms.date: 03/28/2019
topic_type:
- apiref
api_name:
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ae134f37f4a42cf7be91d16333c8856b834c7e35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802015"
---
# <a name="bug-check-0xd1-driver_irql_not_less_or_equal"></a>Bug 检查0xD1：驱动程序 \_ IRQL \_ 不 \_ 小于 \_ 或 \_ 等于


驱动程序 \_ IRQL \_ 不 \_ 小于 \_ 或 \_ 等于 Bug 检查的值为0x000000D1。 这表示内核模式驱动程序尝试在进程 IRQL 太高时访问可分页内存。 

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_irql_not_less_or_equal-parameters"></a>驱动程序 \_ IRQL \_ 不 \_ 小于 \_ 或 \_ 等于参数

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
<td align="left"><p>1</p></td>
<td align="left"><p>引用的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>引用时 IRQL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><ul>
<li>0-读取</li>
<li>1-写入</li>
<li>2-执行</li>
<li>8-执行</li>
</td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>处理引用的内存。 使用<a href="./ln--list-nearest-symbols-.md"> <strong>ln</strong> (列出此地址最近) 的符号</a>，以查看函数的名称。</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

通常情况下，当发生此错误时，驱动程序已尝试访问可分页 (或完全无效的地址) 而中断请求级别 (IRQL) 太高。 这可能是由于：

 - 在 DISPATCH_LEVEL 或更高版本上执行时，取消引用错误指针 (例如 NULL 或释放的指针) 。

 - 访问 DISPATCH_LEVEL 的或更高版本的可分页数据。

 - 在 DISPATCH_LEVEL 或更高版本上执行可分页代码。

如果可以识别负责错误的驱动程序，则其名称将打印在蓝色屏幕上，并存储在内存中 (PUNICODE \_ 字符串) **KiBugCheckDriver** 的位置。 可以使用 [ **dx** (显示调试器对象模型表达式)](dx--display-visualizer-variables-.md)（一个调试器命令）来显示此内容： **dx KiBugCheckDriver**。

此 bug 检查通常是由于使用了不正确的内存地址的驱动程序引起的。

页面错误的可能原因包括以下事件：

- 该函数被标记为可分页并在提升的 IRQL (上运行，这包括获取锁定) 。

- 对另一驱动程序中的函数调用了函数，但该驱动程序已卸载。

- 此函数是通过使用无效指针的函数指针调用的。


<a name="resolution"></a>解决方法
----------

如果此问题是由您正在开发的驱动程序引起的，请确保在 bug 检查时执行的函数 (1) 未标记为可分页或 (2) 不调用任何其他可能分页的内联函数。

[**！分析**](-analyze.md)调试器扩展显示有关 bug 检查的信息，可帮助确定根本原因。 下面的示例是来自 **！分析** 的输出。

```dbgcmd
DRIVER_IRQL_NOT_LESS_OR_EQUAL (d1)
An attempt was made to access a pageable (or completely invalid) address at an
interrupt request level (IRQL) that is too high.  This is usually
caused by drivers using improper addresses.
If kernel debugger is available get stack backtrace.
Arguments:
Arg1: fffff808add27150, memory referenced
Arg2: 0000000000000002, IRQL
Arg3: 0000000000000000, value 0 = read operation, 1 = write operation
Arg4: fffff808adc386a6, address which referenced memory
```

如果转储文件中有陷阱帧，请使用 [**陷井**](-trap--display-trap-frame-.md) 命令将上下文设置为提供的地址。

若要开始调试此类 bug 检查，请使用 [ **k**、 **kb**、 **Glm-kc-qnw**、 **kd**、 **kp**、 **kp**、 **kv** (显示 stack backtrace)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令来检查堆栈跟踪。

在调试器中，运行 [**！！ irql**](-irql.md) 命令以显示有关在调试器中断之前目标计算机上的处理器的 irql 的信息。 例如：

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

在大多数情况下，这种类型的 bug 检查都不是 IRQL 级别，而是要访问的内存。

由于此 bug 检查通常是由于使用了不正确的内存地址的驱动程序引起的，因此请使用参数1、3和4进一步进行调查。

使用 [ **ln** (列出最接近)](ln--list-nearest-symbols-.md)参数4的符号，以查看调用的函数的名称。 另外，请检查 **！分析** 输出，查看是否确定了错误代码。

使用参数1的 " [**！ pool**](-pool.md) " 地址，查看其是否为页面缓冲池。 使用 [**！ address**](-address.md) 和 advanced [**！ pte**](-pte.md) 命令了解有关此内存区域的详细信息。

使用 " [显示内存](-db---dc---dd---dp---dq---du---dw.md) " 命令检查参数1的命令中引用的内存。

使用 [ **u**， **ub**， **uu** (unassemble)](u--unassemble-.md)命令查看地址中引用了参数4中的内存的代码。

使用命令 `lm t n` 列出在内存中加载的模块。 使用 [**！ memusage**](-memusage.md) 和检查系统内存的一般状态。 


### <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证程序是一个实时运行的工具，用于检查驱动程序的行为。 例如，驱动程序验证程序检查内存资源（如内存池）的使用。 如果它标识了驱动程序代码执行过程中的错误，它会主动创建一个例外，以允许进一步审查驱动程序代码的一部分。 驱动程序验证程序管理器内置于 Windows 中，在所有 Windows Pc 上都可用。

若要启动驱动程序验证程序管理器，请在命令提示符下键入 **Verifier** 。 你可以配置要验证的驱动程序。 验证驱动程序的代码会在运行时增加开销，因此请尝试验证尽可能少的驱动程序。 有关详细信息，请参阅[驱动程序验证程序](../devtest/driver-verifier.md)。


<a name="remarks"></a>备注
-------

如果你不具备使用 Windows 调试器来处理此问题，则可以使用一些基本的故障排除技术。

- 查看事件查看器中的系统日志，以获取可能有助于识别导致此错误检查的设备或驱动程序的其他错误消息。

- 如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

- 确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在 [Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

有关其他常规疑难解答信息，请参阅 [蓝屏数据](blue-screen-data.md)。
