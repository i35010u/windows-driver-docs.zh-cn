---
title: 中断同步对象
description: 中断同步对象
ms.assetid: c9e228e0-6178-442d-a82a-6b14ed67c9d2
keywords:
- 帮助程序对象 WDK 音频，中断同步对象
- 中断同步对象 WDK 音频
- IInterruptSync 接口
- 同步 WDK 音频
- 中断服务例程 WDK 音频
- Isr WDK 音频
- 非中断例程 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2f98ccb047e69d690fff296dd8500ebff5c4299
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543283"
---
# <a name="interrupt-sync-objects"></a>中断同步对象


## <span id="interrupt_sync_objects"></span><span id="INTERRUPT_SYNC_OBJECTS"></span>


PortCls 系统驱动程序实现[IInterruptSync](https://msdn.microsoft.com/library/windows/hardware/ff536590)为了方便微型端口驱动程序的接口。 **IInterruptSync**表示与非中断例程同步的一系列中断服务例程 (Isr) 执行的中断同步对象。

中断同步对象提供了两个主要功能：

-   执行的中断响应 Isr 的列表。 同步对象连接到不受中断的源。 每次发生中断时，同步对象中指定的顺序，根据所选模式执行 Isr。 （请参阅以下三种模式的说明。）

-   不是 Isr 的例程的执行。 这些非中断例程未连接到同步对象的中断。 相反，非中断例程在调用方的选择的时间运行。 但是，同步对象执行非中断例程以同步方式与 Isr 的对象的列表。 换而言之，非中断例程完成之前运行的同步对象的列表中 Isr 任何开始执行，反之亦然。

中断同步对象是在处理多个 Isr 灵活。 Isr 驻留在同步对象遍历在中断时的链接列表中。 微型端口驱动程序注册时 ISR 的一个同步对象，它指定是否应将 ISR 添加到的开头或此列表的末尾。

微型端口驱动程序调用[ **PcNewInterruptSync** ](https://msdn.microsoft.com/library/windows/hardware/ff537713)函数来创建中断同步对象。 在此调用，该驱动程序指定是用来在中断时遍历 Isr 其列表对象的方式。 在调用支持下表中的 INTERRUPTSYNCMODE 枚举常量指定三个选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Constant</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>InterruptSyncModeNormal</strong></p></td>
<td align="left"><p>每个 ISR 调用列表中，直到其中一个返回 STATUS_SUCCESS。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InterruptSyncModeAll</strong></p></td>
<td align="left"><p>调用列表中的每个 ISR 恰好一次，而不考虑前面 Isr 的返回代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InterruptSyncModeRepeat</strong></p></td>
<td align="left"><p>直到行程通过列表发生在列表中的没有 ISR 返回 STATUS_SUCCESS 遍历 Isr 的完整列表。</p></td>
</tr>
</tbody>
</table>

 

在中**InterruptSyncModeNormal**模式下，同步对象将调用每个 ISR 列表中，直到其中一个返回状态\_成功。 不调用列表，请按照此 ISR 任何 Isr。 此模式来模拟操作系统通常处理 Isr 的方式。 如果没有任何 Isr 返回状态\_成功后，行为是相同**InterruptSyncModeAll**。

在中**InterruptSyncModeAll**模式下，在列表中的每个 ISR 调用一次，而不考虑前面 Isr 的返回代码。 这适用于更简单的硬件位置中断的源是不确定性的但也可能是在其他情况下也很有用。 例如，可能会在每个中断，而不考虑这两个源的特定中断来自紧密同步两个中断源。

在中**InterruptSyncModeRepeat**模式下，同步对象重复遍历 Isr 的整个列表直到行程通过列表发生在其中没有在列表中的例程将返回状态\_成功。 此模式适合于某些情况下在其中来自多个源的中断可能会被触发相同的中断行上一次或 ISR 处理过程的第二个中断可能会被触发。 每个中断源必须能够确定其是否需要进行处理。 系统将停止响应，如果始终返回状态 ISR\_成功注册的在此模式下一个同步对象。

在任何一种模式，同步对象就会确认到操作系统的中断如果任何已注册 Isr 返回状态\_成功。 在所有三种模式下，如果所有中断源都指示它们未成功处理中断，同步对象将返回成功结果代码到操作系统。

**IInterruptSync**接口支持以下方法：

[**IInterruptSync::CallSynchronizedRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff536592)

[**IInterruptSync::Connect**](https://msdn.microsoft.com/library/windows/hardware/ff536594)

[**IInterruptSync::Disconnect**](https://msdn.microsoft.com/library/windows/hardware/ff536597)

[**IInterruptSync::GetKInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff536599)

[**IInterruptSync::RegisterServiceRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff536600)

 

 




