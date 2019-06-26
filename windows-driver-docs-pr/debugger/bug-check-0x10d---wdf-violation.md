---
title: Bug 检查 0x10D WDF_VIOLATION
description: WDF_VIOLATION bug 检查具有 0x0000010D 值。 这表示内核模式驱动程序框架 (KMDF) 检测到 Windows 基于 framework 的驱动程序中发现错误。
ms.assetid: 2d8c9730-cd24-4f8c-8f8b-252644737847
keywords:
- Bug 检查 0x10D WDF_VIOLATION
- WDF_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WDF_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cee1176f702120588defdbec83d9bf5d08efe7d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367923"
---
# <a name="bug-check-0x10d-wdfviolation"></a>Bug 检查 0x10D：WDF\_冲突


WDF\_冲突错误检查的值为 0x0000010D。 这表示内核模式驱动程序框架 (KMDF) 检测到 Windows 基于 framework 的驱动程序中发现错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="wdfviolation-parameters"></a>WDF\_冲突参数


参数 1 指示错误检查的特定错误代码。 保留参数 4。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>指向 WDF_POWER_ROUTINE_TIMED_OUT_DATA 结构</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>基于框架的驱动程序电源操作期间已超时。 这通常意味着设备堆栈未设置 DO_POWER_PAGABLE 位和驱动程序尝试执行可分页操作后关闭分页设备堆栈。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>正在尝试获取当前持有的锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WDFREQUEST 句柄</p></td>
<td align="left"><p>在这两个缓冲区保留的未完成引用的数目</p></td>
<td align="left"><p>Windows 驱动程序框架验证程序遇到致命错误。 特别是，I/O 请求已完成，但无法删除一个框架请求对象，因为有未完成的引用，到输入的缓冲区、 输出缓冲区，或这两者。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>调用方的地址</p></td>
<td align="left"><p>一个<strong>NULL</strong>参数传递给需要非函数<strong>NULL</strong>值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>中传递的句柄值</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>类型不正确的 framework 对象句柄传递给框架对象方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>请参阅下表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>Framework 对象的句柄</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>驱动程序尝试通过调用错误地删除 framework 对象<strong>WdfObjectDereference</strong>若要删除而不是调用的句柄<strong>WdfObjectDelete</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>DMA 事务对象的句柄</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>DMA 事务对象上的操作发生，而不是处于正确状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>当前未使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>指向 WDF_QUEUE_FATAL_ERROR_DATA 结构的指针</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>处理队列中当前的请求时发生致命错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xB</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>请参阅下表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xC</p></td>
<td align="left"><p>WDFDEVICE 句柄</p></td>
<td align="left"><p>指向新 PnP IRP</p></td>
<td align="left"><p>新的状态更改 PnP IRP 到达该驱动程序处理另一个状态更改 PnP IRP 时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xD</p></td>
<td align="left"><p>WDFDEVICE 句柄</p></td>
<td align="left"><p>指向 power IRP</p></td>
<td align="left"><p>设备的电源策略所有者接收到没有请求的 IRP 的幂。 可能有多个电源策略所有者，但只允许有一个。 KMDF 驱动程序可以通过调用更改电源策略所有权<strong>WdfDeviceInitSetPowerPolicyOwnership</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xE</p></td>
<td align="left"><p>IRQL 事件回调函数调用的。</p></td>
<td align="left"><p>IRQL 事件回调函数返回。</p></td>
<td align="left"><p>一个事件的回调函数未返回在相同的 IRQL 在其中调用它。 回调函数已更改的 IRQL 直接或间接地 （例如，通过获取调节锁，它将提升到 DISPATCH_LEVEL IRQL，但不是释放自旋锁）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xF</p></td>
<td align="left"><p>事件回调函数的地址。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>一个事件的回调函数进入临界区，但未返回之前离开临界区。</p></td>
</tr>
</tbody>
</table>

 

**参数 1 等于 0x6**

如果参数 1 为 0x6，致命错误已处理 WDF 请求中。 在这种情况下，进一步参数 2 指定的错误，类型定义的枚举 WDF\_请求\_致命错误\_错误。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>IRP 的地址</p></td>
<td align="left"><p>没有更多的 I/O 堆栈位置均可设置基础 IRP 的格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>WDF 请求句柄值</p></td>
<td align="left"><p>尝试设置不包含 IRP 的框架请求对象的格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WDF 请求句柄值</p></td>
<td align="left"><p>该驱动程序试图发送已发送到的 I/O 目标 framework 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>尝试写入到 WDR_REQUEST_FATAL_ERROR_INFORMATION_LENGTH_MISMATCH_DATA 结构，其中包含指向 IRP、 WDF 请求句柄值、 IRP 主要函数和字节数的指针的指针</p></td>
<td align="left"><p>驱动程序已完成的框架请求，但具有更多的字节写入输出缓冲区中指定。</p></td>
</tr>
</tbody>
</table>

 

**参数 1 等于 0xB**

如果参数 1 等于 0xB，尝试获取或释放锁的句柄无效。 在这种情况下，参数 3 进一步指定进行的错误。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>句柄值</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>一个句柄传递给<strong>WdfObjectAcquireLock</strong>或<strong>WdfObjectReleaseLock</strong>表示不支持同步锁的对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WDF 数值调节钮锁定句柄</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>即没有获取它的线程被释放自旋锁。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

请参阅每个代码的原因的说明的 Parameters 节中的说明。

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在收集信息，例如出错的代码模块。

通常情况下，WDF 转储文件会进一步产生导致此 bug 检查驱动程序的信息。 使用此命令可查看日志文件。

```dbgcmd
kd> !wdfkd.wdflogdump <WDF_Driver_Name>
```

如果参数 1 等于**0x2**，检查调用方的堆栈，以确定有问题的锁。

如果参数 1 等于**0x3**，驱动程序的内核模式驱动程序框架错误日志将包含有关未完成的引用的详细信息。

如果参数 1 等于**0x4**，使用[ **ln 调试器**](ln--list-nearest-symbols-.md)命令的值与*参数 3*作为其参数来确定函数需要一个非**NULL**参数。

如果参数 1 等于**0x7**，使用 * *！ wdfkd.wdfhandle***Parameter 2*扩展命令，以确定句柄类型。

如果参数 1 等于**0xA**，然后 WDF\_队列\_致命错误\_错误\_数据结构将指示有问题的请求或队列句柄。 它还指示 NTSTATUS，如果不是状态\_成功后，可用时。

 

 




