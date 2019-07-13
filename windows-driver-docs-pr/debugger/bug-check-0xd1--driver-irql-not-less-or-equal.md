---
title: Bug 检查 0xD1 DRIVER_IRQL_NOT_LESS_OR_EQUAL
description: DRIVER_IRQL_NOT_LESS_OR_EQUAL bug 检查具有 0x000000D1 值。 这表示内核模式驱动程序试图访问可分页内存过高的 IRQL 的进程。
ms.assetid: 26cfd881-cc6e-4cc3-b464-e67d75700b96
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
ms.openlocfilehash: c13dd820784cd03a995d42c235fd9074c7d065d9
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866524"
---
# <a name="bug-check-0xd1-driverirqlnotlessorequal"></a>Bug 检查 0xD1：DRIVER\_IRQL\_NOT\_LESS\_OR\_EQUAL


该驱动程序\_IRQL\_不\_较少\_或\_相等 bug 检查的值为 0x000000D1。 这表示内核模式驱动程序尝试访问时进程 IRQL 过高的可分页内存。 

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="driverirqlnotlessorequal-parameters"></a>驱动程序\_IRQL\_不\_较少\_或\_等于参数


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
<td align="left"><p>引用的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL 在引用的时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p>
<p><strong>2:</strong>执行</p>
<p><strong>8:</strong>执行</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>引用内存的地址。 使用此地址上的 ln 以查看该函数的名称。</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

通常情况下，驱动程序尝试访问的可分页 （或者是完全无效） 的地址在 IRQL 是否过高。

这可能是以下原因引起的：

1. 执行处于或高于 DISPATCH_LEVEL 时取消引用错误的指针 （如 NULL 或已释放的指针）。
2. 访问处于或高于 DISPATCH_LEVEL 的可分页数据。
3. 执行可分页代码处于或高于 DISPATCH_LEVEL。

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。 可以使用调试器 dx 命令来显示此- `dx KiBugCheckDriver`。

已用过的不正确的内存地址的驱动程序通常被由于此 bug 检查。

页面错误的可能原因包括：

- 该函数被标记为可分页，并在提升的 IRQL （其中包括获取锁） 运行。

- 另一个驱动程序中的函数执行函数调用，该驱动程序已被卸载。

- 调用函数时使用了无效的指针的函数指针。

<a name="resolution"></a>分辨率
----------

如果问题由正在开发的驱动程序，请确保在检查错误时执行的函数的未标记为可分页或不调用任何其他无法换出的内联函数。

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

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

如果陷阱帧将在转储文件使用`.trap`命令以将上下文设置为所提供的地址。

若要开始，请检查堆栈跟踪使用[ **k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。

使用`!IRQL`命令以显示有关中断请求级别 (IRQL) 的信息在调试器中断之前对目标计算机上的处理器。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

大部分时间问题不是 IRQL 级别，而不是正在访问的内存。

检查此错误通常由已用过的不正确的内存地址的驱动程序引起的因为使用参数 1，3 和 4 到 invesitgate 进一步。

使用[ln （列表最接近符号）](ln--list-nearest-symbols-.md)参数 4，以查看调用的函数的名称。 同时，检查 ！ 分析输出，以查看是否标识在出错的代码。

使用[！ 池](-pool.md)上以查看是否分页的参数 1 地址池。 使用[！ 地址](-address.md)和高级[！ pte](-pte.md)命令，若要详细了解此区域中的内存。

使用[显示内存](-db---dc---dd---dp---dq---du---dw.md)命令来检查在参数 1 中的命令中引用的内存。

使用[反汇编](u--unassemble-.md)命令以查看代码中引用参数 4 中的内存的地址。

使用`lm t n`到内存中加载的模块列表。 使用[！ memusage](-memusage.md)并检查系统内存的一般状态。 

**驱动程序验证程序**

驱动程序验证程序是一种工具，运行实时检查驱动程序的行为。 例如，驱动程序验证工具将检查内存资源，如内存池的使用。 如果它发现错误的驱动程序代码执行过程中，它会主动创建例外以允许驱动程序代码以进行进一步仔细检查该部分。 驱动程序验证程序管理器内置于 Windows，可在所有 Windows Pc 上。 若要启动驱动程序验证程序管理器，请键入*Verifer*在命令提示符。 可以配置你想要验证的驱动程序。 验证驱动程序的代码将添加开销在运行，因此请尝试并验证尽可能最少数量的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。

<a name="remarks"></a>备注
-------

如果您不准备使用 Windows 调试器处理此问题，可以使用一些基本的故障排除方法。

- 检查事件查看器中的系统日志可能有助于识别设备或驱动程序导致此错误检查的其他错误消息。

- 如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

- 确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

- 有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。
