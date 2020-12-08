---
title: Bug 检查 0x10D WDF_VIOLATION
description: WDF_VIOLATION bug 检查的值为0x0000010D。 这表明 Kernel-Mode Driver Framework (KMDF) 检测到 Windows 在基于框架的驱动程序中发现了错误。
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
ms.openlocfilehash: 2d388b284eeb20040e72519eea70cd14aef60307
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804005"
---
# <a name="bug-check-0x10d-wdf_violation"></a>Bug 检查0x10D： WDF \_ 冲突


WDF \_ 冲突 bug 检查的值为0x0000010D。 这表明 Kernel-Mode Driver Framework (KMDF) 检测到 Windows 在基于框架的驱动程序中发现了错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="wdf_violation-parameters"></a>WDF \_ 冲突参数


参数1指示 bug 检查的特定错误代码。 参数4为保留参数。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>指向 WDF_POWER_ROUTINE_TIMED_OUT_DATA 结构的指针</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>基于框架的驱动程序在执行电源操作时超时。 这通常意味着设备堆栈未设置 DO_POWER_PAGABLE 位，驱动程序在关闭分页设备堆栈后尝试执行可分页操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>尝试获取当前正在持有的锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WDFREQUEST 句柄</p></td>
<td align="left"><p>同时保留在两个缓冲区上的未处理引用数</p></td>
<td align="left"><p>Windows Driver Framework 验证程序遇到错误。 特别是，i/o 请求已完成，但无法删除框架请求对象，因为存在对输入缓冲区和/或输出缓冲区的未处理引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>调用方的地址</p></td>
<td align="left"><p>向函数传递的 <strong>NULL</strong> 参数需要非<strong>NULL</strong> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>传入的句柄值</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>向框架对象方法传递了错误类型的框架对象句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>请参阅下表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>框架对象的句柄</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>驱动程序试图通过调用 <strong>WdfObjectDereference</strong> 来删除一个句柄而不是调用 <strong>WdfObjectDelete</strong>来尝试错误地删除框架对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>DMA 事务对象的句柄</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>当 DMA 事务对象的状态不正确时，操作发生。</p></td>
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
<td align="left"><p>预留</p></td>
<td align="left"><p>处理队列中当前存在的请求时出现错误。</p></td>
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
<td align="left"><p>指向新 PnP IRP 的指针</p></td>
<td align="left"><p>当驱动程序正在处理另一个状态更改 PnP IRP 时，会收到新的状态更改 PnP IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xD</p></td>
<td align="left"><p>WDFDEVICE 句柄</p></td>
<td align="left"><p>指向电源 IRP 的指针</p></td>
<td align="left"><p>设备的电源策略所有者收到了未请求的 power IRP。 可能有多个电源策略所有者，但只允许使用一个。 KMDF 驱动程序可以通过调用 <strong>WdfDeviceInitSetPowerPolicyOwnership</strong>更改电源策略所有权。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xE</p></td>
<td align="left"><p>调用事件回调函数的 IRQL。</p></td>
<td align="left"><p>事件回调函数返回的 IRQL。</p></td>
<td align="left"><p>事件回调函数未返回与调用该函数的 IRQL 相同的情况。 回调函数会直接或间接地更改 IRQL (例如，通过获取旋转锁，这会引发 IRQL 来 DISPATCH_LEVEL，但不会释放旋转锁) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xF</p></td>
<td align="left"><p>事件回调函数的地址。</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>事件回调函数进入了一个关键区域，但它未在返回前离开关键区域。</p></td>
</tr>
</tbody>
</table>

 

**参数1等于0x6**

如果参数1等于0x6，则在处理 WDF 请求时出错。 在这种情况下，参数2进一步指定了由枚举 WDF 请求错误所定义的错误的类型 \_ \_ \_ 。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>IRP 的地址</p></td>
<td align="left"><p>没有更多的 i/o 堆栈位置可用于设置基础 IRP 的格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>WDF 请求句柄值</p></td>
<td align="left"><p>尝试对不包含 IRP 的框架请求对象进行格式设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WDF 请求句柄值</p></td>
<td align="left"><p>驱动程序尝试发送已发送到 i/o 目标的框架请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>指向 WDR_REQUEST_FATAL_ERROR_INFORMATION_LENGTH_MISMATCH_DATA 结构的指针，该结构包含一个指向 IRP 的指针、一个 WDF 请求句柄值、一个 IRP 主函数和尝试写入的字节数</p></td>
<td align="left"><p>驱动程序已经完成框架请求，但写入到输出缓冲区的字节比 IRP 中指定的多。</p></td>
</tr>
</tbody>
</table>

 

**参数1等于0xB**

如果参数1等于0xB，则尝试获取或释放锁定是无效的。 在这种情况下，参数3会进一步指定已进行的错误。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>句柄值</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>传递给 <strong>WdfObjectAcquireLock</strong> 或 <strong>WdfObjectReleaseLock</strong> 的句柄表示不支持同步锁定的对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WDF 旋转锁句柄</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>旋转锁正在由未获取它的线程释放。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

有关原因的说明，请参阅参数部分中每个代码的说明。

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助收集信息，如出错代码模块。

通常，WDF 转储文件将生成有关导致此错误检查的驱动程序的详细信息。 使用此命令查看日志文件。

```dbgcmd
kd> !wdfkd.wdflogdump <WDF_Driver_Name>
```

如果参数1等于 **0x2**，则检查调用方的堆栈以确定有问题的锁。

如果参数1等于 **0x3**，则驱动程序的 Kernel-Mode driver Framework 错误日志将包含有关未完成引用的详细信息。

如果参数1等于 **0x4**，请使用 *参数为 3* 的值为的 [**ln 调试器**](ln--list-nearest-symbols-.md)命令作为其参数，以确定哪一个函数需要非 **空** 参数。

如果参数1等于 **0x7**，请使用 **！ wdfkd**_参数 2_ 扩展命令来确定句柄类型。

如果参数1等于 **0xA**，则 WDF \_ 队列 \_ 严重 \_ 错误 \_ 数据结构将指示有问题的请求或队列句柄。 如果状态为 "成功"，则它还将指示 NTSTATUS （如果 \_ 可用）。

 

 




