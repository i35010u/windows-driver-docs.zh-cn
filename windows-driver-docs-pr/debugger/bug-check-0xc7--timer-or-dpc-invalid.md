---
title: Bug 检查 0xC7 TIMER_OR_DPC_INVALID
description: TIMER_OR_DPC_INVALID bug 检查的值为0x000000C7。 如果在不允许的情况下在内存的某个位置找到了 (DPC) 的内核计时器或延迟过程调用，则会发出此情况。
keywords:
- Bug 检查 0xC7 TIMER_OR_DPC_INVALID
- TIMER_OR_DPC_INVALID
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TIMER_OR_DPC_INVALID
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 671fcd840bd5518b9f7a3b05a5d3ab9ed97c030a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838831"
---
# <a name="bug-check-0xc7-timer_or_dpc_invalid"></a>Bug 检查0xC7：计时器 \_ 或 \_ DPC \_ 无效


计时器 \_ 或 \_ DPC \_ 无效 bug 检查的值为0x000000C7。 如果在不允许的情况下在内存的某个位置找到了 (DPC) 的内核计时器或延迟过程调用，则会发出此情况。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="timer_or_dpc_invalid-parameters"></a>计时器 \_ 或 \_ DPC \_ 无效参数


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
<td align="left"><p>0x0</p></td>
<td align="left"><p>Timer 对象的地址</p></td>
<td align="left"><p>正在检查的内存范围的开始部分</p></td>
<td align="left"><p>正在检查的内存范围结束时间</p></td>
<td align="left"><p>计时器对象位于内存块中，但不允许 timer 对象。 .</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>DPC 对象的地址</p></td>
<td align="left"><p>正在检查的内存范围的开始部分</p></td>
<td align="left"><p>正在检查的内存范围结束时间</p></td>
<td align="left"><p>在不允许 DPC 对象的内存块中找到了 DPC 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>DPC 例程的地址</p></td>
<td align="left"><p>正在检查的内存范围的开始部分</p></td>
<td align="left"><p>正在检查的内存范围结束时间</p></td>
<td align="left"><p>在不允许 DPC 对象的内存块中找到了 DPC 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>DPC 对象的地址</p></td>
<td align="left"><p>处理器编号</p></td>
<td align="left"><p>系统中的处理器数</p></td>
<td align="left"><p>DPC 对象的处理器编号不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>DPC 例程的地址</p></td>
<td align="left"><p>内核调用 DPC 例程之前线程的 APC 禁用计数</p></td>
<td align="left"><p>调用 DPC 例程后线程的 APC 禁用计数</p></td>
<td align="left"><p>在 DPC 例程执行过程中，线程的 APC 禁用计数已更改。</p>
<p>每次驱动程序调用 <strong>KeEnterCriticalRegion</strong>、 <strong>FsRtlEnterFileSystem</strong>或获取互斥体时，APC 禁用计数都将减少。</p>
<p>每次驱动程序调用 <strong>KeLeaveCriticalRegion</strong>、 <strong>KeReleaseMutex</strong>或 <strong>FsRtlExitFileSystem</strong>时，APC 禁用计数都将递增。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>DPC 例程的地址</p></td>
<td align="left"><p>内核调用 DPC 例程之前线程的 APC 禁用计数</p></td>
<td align="left"><p>调用 DPC 例程后线程的 APC 禁用计数</p></td>
<td align="left"><p>线程的 APC 禁用计数在计时器 DPC 例程执行期间发生了更改。</p>
<p>每次驱动程序调用 <strong>KeEnterCriticalRegion</strong>、 <strong>FsRtlEnterFileSystem</strong>或获取互斥体时，APC 禁用计数都将减少。</p>
<p>每次驱动程序调用 <strong>KeLeaveCriticalRegion</strong>、 <strong>KeReleaseMutex</strong>或 <strong>FsRtlExitFileSystem</strong>时，APC 禁用计数都将递增。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

这种情况通常是由驱动程序在释放其所驻留的内存之前未能取消计时器或 DPC 导致的。

<a name="resolution"></a>解决方法
----------

如果您是驱动程序编写者，请使用通过此 bug 检查获取的信息来修复代码中的 bug。

如果你是系统管理员，如果问题仍然存在，则应卸载该驱动程序。

 

 




