---
title: 等待和 Apc
description: 等待和 Apc
ms.assetid: b967beec-922c-4acf-a578-c476ce024fdb
keywords:
- 内核调度程序对象 WDK，警报
- 调度程序对象 WDK 内核警报
- Apc WDK 内核
- 警报 WDK 内核
- 内核调度程序对象 WDK Apc
- 调度程序对象 WDK 内核 Apc
- 可报警参数
- WaitMode 参数
- 内核调度程序对象 WDK，等待
- 调度程序对象 WDK 内核等待
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5536a081e269ab3905e3f080030f4ae77d20d2a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555307"
---
# <a name="waits-and-apcs"></a>等待和 Apc





等待调度程序对象代表用户模式下调用方的线程必须做好该等待会中断用户 APC 或线程终止。 当线程调用[ **KeWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff553350)， [ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)， [ **KeWaitForMutexObject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)，或[ **KeDelayExecutionThread**](https://msdn.microsoft.com/library/windows/hardware/ff551986)，操作系统可以置于等待状态的线程。 通常情况下，该线程将一直处于等待状态直到操作系统可以完成操作，调用方请求。 但是，如果调用方指定*WaitMode* = UserMode，操作系统可能会中断等待。 在这种情况下，状态的 NTSTATUS 值退出例程\_用户\_APC。

任何驱动程序，它调用了一个与前面的四种例程*WaitMode* = UserMode 必须准备好接收状态的返回值\_用户\_APC。 该驱动程序必须完成当前操作状态\_用户\_APC 并将控制权返回到用户模式。

在其中操作系统中断等待的确切情况取决于值*Alertable*例程的参数。 如果*Alertable* = **TRUE**，则等待是可报警等待。 否则，则等待是非可报警等待。 操作系统会中断可报警等待只是为了提供用户 APC。 操作系统会中断这两种类型的等待时间，从而终止该线程。

下表介绍了不同的参数设置、 等待与用户 APC 传递之间的关系。

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
<th>用户 APC 传递？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>Alertable</em> = <strong>TRUE</strong>
<em>WaitMode</em> = <strong>UserMode</strong></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><em>Alertable</em> = <strong>TRUE</strong>
<em>WaitMode</em> = <strong>KernelMode</strong></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><em>Alertable</em> = <strong>FALSE</strong>
<em>WaitMode</em> = <strong>UserMode</strong></td>
<td><p>是的有关线程终止。 不可以，出于用户 Apc。</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><em>Alertable</em> = <strong>FALSE</strong>
<em>WaitMode</em> = <strong>KernelMode</strong></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>

 

您可以禁用线程内核 Apc。 如果您禁用了线程内核 Apc，用户 APC 交付和该线程的线程终止也被禁用。 有关如何禁用 Apc 的详细信息，请参阅[禁用 Apc](disabling-apcs.md)。

警报，很少使用的操作系统，内部的机制，还可以中断可报警等待状态。 警报可以中断等待时*Alertable* = **TRUE**、 的值而不考虑*WaitMode*参数。 等待例程将返回状态的值\_ALERTED。

请注意，内核 Apc 运行抢先，并且不会导致**KeWaitFor * Xxx*** 或**KeDelayExecutionThread**返回。 系统中断，并在内部继续等待。 驱动程序不正常情况下受此过程中，但很可能错过的暂时性条件，如调用的调度程序对象信号的驱动程序[ **KePulseEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552979)。

 

 




