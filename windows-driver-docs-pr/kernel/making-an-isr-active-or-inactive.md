---
title: 使 ISR 处于活动或非活动状态
description: 从 Windows 8 开始，驱动程序可以调用 IoReportInterruptActive 或 IoReportInterruptInactive 例程，使已注册的中断服务例程 (ISR) 活动或非活动状态。
ms.assetid: 788D9341-D1F8-4126-8C30-AA49DE27F4BB
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 97fc698357cbdc04179e3a3b4dcc2239cea00bc9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187585"
---
# <a name="making-an-isr-active-or-inactive"></a>使 ISR 处于活动或非活动状态


从 Windows 8 开始，驱动程序可以调用 [**IoReportInterruptActive**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreportinterruptactive) 或 [**IoReportInterruptInactive**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreportinterruptinactive) 例程，使已注册的中断服务例程 (ISR) 活动或非活动状态。

若要注册 ISR，并将 ISR 连接到一个或一组中断，驱动程序将调用 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 例程。 注册 ISR 后，驱动程序可以使用 **IoReportInterruptActive** 和 **IoReportInterruptInactive** 来执行轻型 (或 "软" ) 连接并断开 ISR 注册，使其保持不变。 **IoReportInterruptInactive** 通过软断开关联的中断或中断来禁用对 ISR 的调用。 **IoReportInterruptActive** 软-连接这些中断以启用对 ISR 的调用。

例如，驱动程序可以调用 **IoReportInterruptInactive** ，在设备退出 D0 电源状态之前软断开一组中断，并调用 **IoReportInterruptActive** 在设备重新输入 D0 后软连接这些中断。 原则上，驱动程序可以在设备退出 D0 之前调用 [**IoDisconnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex) ，并在设备重新输入 d0 后调用 **IoConnectInterruptEx** 。 但是， **IoReportInterrupt * Xxx*** 调用比 **IoConnectInterruptEx** 和 **IoDisconnectInterruptEx** 调用更快。 与 **IoConnectInterruptEx** 和 **IoDisconnectInterruptEx** 调用相比，这种情况可能因多种原因而失败 (例如，系统资源不足) ， **IoReportInterrupt * Xxx*** 调用很少发生，但可能会失败。 此外，可以在 IRQL = 调度级别调用 **IoReportInterrupt * Xxx*** 例程 &lt; \_ ，而只能在被动级别调用 **IoConnectInterruptEx** 和 **IoDisconnectInterruptEx** \_ 。

默认情况下，ISR 处于活动状态 (在 **IoConnectInterruptEx** 成功注册 isr 后) 启用对 isr 的调用。

调用 **IoReportInterruptInactive** 和 **IoReportInterruptActive** 是可选的。 如果驱动程序永远不会调用这些例程，则已注册的 ISR 会保持活动状态，直到驱动程序调用 [**IoDisconnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterruptex) 例程来取消注册 ISR。

驱动程序应将设备配置为仅当这些中断的 ISR 处于活动状态时才发出中断。 当 ISR 处于非活动状态时，无法阻止设备发出中断可能会导致系统不稳定。 例如，如果设备与其他设备共享级别触发的中断线路，并且设备在 ISR 处于非活动状态时发出中断请求，则线路上其他设备的 Isr 不会确认中断，中断将继续激发。 在调用 **IoReportInterruptInactive**之前，驱动程序应将设备配置为停止发出中断。 调用 **IoReportInterruptActive**之后，驱动程序应将设备配置为开始发出中断。

若要注销 ISR，无论 ISR 当前处于活动状态还是非活动状态，驱动程序都可以调用 **IoDisconnectInterruptEx** 。

ISR 已经处于活动状态时出现的 **IoReportInterruptActive** 调用不起作用，但不会被视为错误。 同样，当 ISR 已经处于非活动状态时，就不 **会有任何** 影响，但不会被视为错误。

 

