---
title: 等待和 APC
description: 等待和 APC
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
ms.openlocfilehash: a0bc8acd6216b5b2c5bffbd7b645d23772ea8dba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820623"
---
# <a name="waits-and-apcs"></a>等待和 APC





对于代表用户模式调用方等待发送器对象的线程，必须准备好等待该等待被用户 APC 或线程终止中断。 当线程调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)、 [**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)、 [**KeWaitForMutexObject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)或 [**KeDelayExecutionThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)时，操作系统可将线程置于等待状态。 通常情况下，线程仍处于等待状态，直到操作系统能够完成调用方请求的操作。 但是，如果调用方指定 *WaitMode* = UserMode，则操作系统可能会中断等待。 在这种情况下，例程将以状态 USER APC 的 NTSTATUS 值退出 \_ \_ 。

使用 *WaitMode* = UserMode 调用前面四个例程之一的任何驱动程序必须准备好接收状态用户 APC 的返回值 \_ \_ 。 驱动程序必须完成其当前操作，状态为 \_ user \_ APC，并将控制返回到用户模式。

操作系统中断等待的确切情况取决于例程的 *可报警* 参数的值。 如果 *可报警*  =  **为 TRUE**，则等待是可报警等待。 否则，等待是可报警的等待。 操作系统中断可报警仅等待为用户提供 APC。 操作系统中断两种等待来终止线程。

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
<td><em>可报警</em>  = <strong>TRUE</strong>
<em>WaitMode</em>  =  <strong>UserMode</strong></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><em>可报警</em>  = <strong>TRUE</strong>
<em>WaitMode</em>  =  <strong>KernelMode</strong></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><em>可报警</em>  = <strong>FALSE</strong>
<em>WaitMode</em>  =  <strong>UserMode</strong></td>
<td><p>是，用于线程终止。 否，适用于用户 Apc。</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><em>可报警</em>  = <strong>FALSE</strong>
<em>WaitMode</em>  =  <strong>KernelMode</strong></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>

 

可以为线程禁用内核 Apc。 如果对某个线程禁用内核 Apc，则该线程的用户 APC 传递和线程终止也会被禁用。 有关如何禁用 Apc 的详细信息，请参阅 [禁用 apc](disabling-apcs.md)。

警报是操作系统内部的一种很少使用的机制，还可以中断可报警等待状态。 当 *可报警*  =  **为 TRUE** 时，无论 *WaitMode* 参数的值如何，警报都可以中断等待。 等待例程返回状态为 "已发出警报" 的值 \_ 。

请注意，内核 Apc 运行提前，而不会导致 **KeWaitFor * Xxx*** 或 **KeDelayExecutionThread** 返回。 系统中断并在内部恢复等待。 驱动程序通常不受此过程的影响，但驱动程序可能会为暂时性情况（如对 [**KePulseEvent**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent)的调用）丢失调度程序对象信号。

 

