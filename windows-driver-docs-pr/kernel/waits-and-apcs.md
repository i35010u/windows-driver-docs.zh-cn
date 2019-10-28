---
title: 等待和 APC
description: 等待和 APC
ms.assetid: b967beec-922c-4acf-a578-c476ce024fdb
keywords:
- 内核调度程序对象 WDK，警报
- 调度程序对象 WDK 内核，警报
- Apc WDK 内核
- 警报 WDK 内核
- 内核调度程序对象 WDK，Apc
- 调度程序对象 WDK 内核，Apc
- 可报警参数
- WaitMode 参数
- 内核调度程序对象 WDK，等待
- 调度程序对象 WDK 内核，等待
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6103b4f319cee1d3d16d60832cb57fffd910a2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838322"
---
# <a name="waits-and-apcs"></a>等待和 APC





对于代表用户模式调用方等待发送器对象的线程，必须准备好等待该等待被用户 APC 或线程终止中断。 当线程调用[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)、 [**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)、 [**KeWaitForMutexObject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)或[**KeDelayExecutionThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)时，操作系统可将线程置于等待状态。 通常情况下，线程仍处于等待状态，直到操作系统能够完成调用方请求的操作。 但是，如果调用方指定*WaitMode* = UserMode，则操作系统可能会中断等待。 在这种情况下，例程使用状态\_用户\_APC 上的 NTSTATUS 值退出。

使用*WaitMode* = UserMode 调用前面四个例程之一的任何驱动程序必须准备好接收\_APC\_状态的返回值。 驱动程序必须完成其当前操作，状态\_用户\_APC，并将控制返回到用户模式。

操作系统中断等待的确切情况取决于例程的*可报警*参数的值。 如果*可报警* = **TRUE**，则等待是可报警等待。 否则，等待是可报警的等待。 操作系统中断可报警仅等待为用户提供 APC。 操作系统中断两种等待来终止线程。

下表说明了不同参数设置、等待和用户 APC 传递之间的关系。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>等待中断？</th>
<th>用户 APC 的交付？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>可报警</em> = <strong>TRUE</strong>
<em>WaitMode</em> = <strong>UserMode</strong></td>
<td><p>“是”</p></td>
<td><p>“是”</p></td>
</tr>
<tr class="even">
<td><em>可报警</em> = <strong>TRUE</strong>
<em>WaitMode</em> = <strong>KernelMode</strong></td>
<td><p>“是”</p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><em>可报警</em> = <strong>FALSE</strong>
<em>WaitMode</em> = <strong>UserMode</strong></td>
<td><p>是，用于线程终止。 否，适用于用户 Apc。</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><em>可报警</em> = <strong>FALSE</strong>
<em>WaitMode</em> = <strong>KernelMode</strong></td>
<td><p>无</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

可以为线程禁用内核 Apc。 如果对某个线程禁用内核 Apc，则该线程的用户 APC 传递和线程终止也会被禁用。 有关如何禁用 Apc 的详细信息，请参阅[禁用 apc](disabling-apcs.md)。

警报是操作系统内部的一种很少使用的机制，还可以中断可报警等待状态。 *可报警* = **TRUE**时，无论*WaitMode*参数的值如何，警报都可以中断等待。 等待例程返回\_警报的状态值。

请注意，内核 Apc 运行提前，而不会导致**KeWaitFor * Xxx*** 或**KeDelayExecutionThread**返回。 系统中断并在内部恢复等待。 驱动程序通常不受此过程的影响，但驱动程序可能会为暂时性情况（如对[**KePulseEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent)的调用）丢失调度程序对象信号。

 

 




