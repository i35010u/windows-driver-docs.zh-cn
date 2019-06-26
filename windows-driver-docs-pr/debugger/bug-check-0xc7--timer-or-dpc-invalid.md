---
title: Bug 检查 0xc7:sp TIMER_OR_DPC_INVALID
description: TIMER_OR_DPC_INVALID bug 检查具有 0x000000C7 值。 这发出如果内核计时器或延迟的过程调用 (DPC) 在其中不允许的内存中的某处找到。
ms.assetid: 25a85b38-c299-4bf8-a7ed-f516adb5fcb1
keywords:
- Bug 检查 0xc7:sp TIMER_OR_DPC_INVALID
- TIMER_OR_DPC_INVALID
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TIMER_OR_DPC_INVALID
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 38bb1e52ca075e84b628ee7a361f3faf0cd80bb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367179"
---
# <a name="bug-check-0xc7-timerordpcinvalid"></a>Bug 检查 0xC7：计时器\_或者\_DPC\_无效


计时器\_或者\_DPC\_无效错误检查的值为 0x000000C7。 这发出如果内核计时器或延迟的过程调用 (DPC) 在其中不允许的内存中的某处找到。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="timerordpcinvalid-parameters"></a>计时器\_或者\_DPC\_无效的参数


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
<td align="left"><p>0x0</p></td>
<td align="left"><p>计时器对象的地址</p></td>
<td align="left"><p>正在检查的内存范围的开始</p></td>
<td align="left"><p>正在检查的内存范围的结尾</p></td>
<td align="left"><p>在计时器对象不允许的内存块中找到该计时器对象。 .</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>DPC 对象的地址</p></td>
<td align="left"><p>正在检查的内存范围的开始</p></td>
<td align="left"><p>正在检查的内存范围的结尾</p></td>
<td align="left"><p>中的 DPC 对象不允许的内存块找 DPC 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>DPC 例程的地址</p></td>
<td align="left"><p>正在检查的内存范围的开始</p></td>
<td align="left"><p>正在检查的内存范围的结尾</p></td>
<td align="left"><p>DPC 例程不允许 DPC 对象的内存块中找到。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>DPC 对象的地址</p></td>
<td align="left"><p>处理器数</p></td>
<td align="left"><p>在系统中的处理器数</p></td>
<td align="left"><p>DPC 对象处理器数不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>DPC 例程的地址</p></td>
<td align="left"><p>线程的 APC 内核调用 DPC 例程之前，请禁用计数</p></td>
<td align="left"><p>线程的 APC DPC 例程在调用之后禁用计数</p></td>
<td align="left"><p>在 DPC 例程执行过程中更改线程的 APC 禁用计数。</p>
<p>APC 禁用计数将减少每次将驱动程序调用<strong>KeEnterCriticalRegion</strong>， <strong>FsRtlEnterFileSystem</strong>，或获取互斥锁。</p>
<p>APC 禁用计数每的次递增一个驱动程序调用<strong>KeLeaveCriticalRegion</strong>， <strong>KeReleaseMutex</strong>，或<strong>FsRtlExitFileSystem</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>DPC 例程的地址</p></td>
<td align="left"><p>线程的 APC 内核调用 DPC 例程之前，请禁用计数</p></td>
<td align="left"><p>线程的 APC DPC 例程在调用之后禁用计数</p></td>
<td align="left"><p>在计时器 DPC 例程的执行过程中更改线程的 APC 禁用计数。</p>
<p>APC 禁用计数将减少每次将驱动程序调用<strong>KeEnterCriticalRegion</strong>， <strong>FsRtlEnterFileSystem</strong>，或获取互斥锁。</p>
<p>APC 禁用计数每的次递增一个驱动程序调用<strong>KeLeaveCriticalRegion</strong>， <strong>KeReleaseMutex</strong>，或<strong>FsRtlExitFileSystem</strong>。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

这种情况通常是由驱动程序无法释放它所在的内存之前取消计时器或 DPC 引起的。

<a name="resolution"></a>分辨率
----------

如果你是驱动程序编写器，使用通过此 bug 检查获取的信息以在代码中修复的错误。

如果你是系统管理员，应卸载该驱动程序，如果问题仍然存在。

 

 




