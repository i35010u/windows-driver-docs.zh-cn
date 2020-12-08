---
title: 处理 SD 卡中断
description: 处理 SD 卡中断
keywords:
- SD WDK 总线，中断
- 中断 WDK SD 总线
- IRQLs WDK SD 总线
- 硬件中断 WDK SD 总线
- 中断通知 WDK SD 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9d0c641b755ff142f2b53af5ca5c9841354a4a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831127"
---
# <a name="handling-sd-card-interrupts"></a>处理 SD 卡中断


安全数字 (SD) 卡驱动程序 () Isr 的中断服务例程，并且它们不获取中断请求 (IRQ) 资源。 SD bus 驱动程序检测并截获硬件中断，然后通过中断通知回调例程 [**PSDBUS \_ 回调 \_ 例程**](/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-sdbus_callback_routine)将它们报告给设备驱动程序，如 [安全数字 (SD) 驱动程序堆栈](./sd-card-driver-stack.md) 和 [打开和初始化 SD 总线接口](./opening--initializing-and-closing-an-sd-card-bus-interface.md)部分中所述。

设备驱动程序无需在中断通知回调例程的上下文中完成中断处理。 驱动程序可以从回调例程返回并在其自身的上下文中完成中断处理。 当驱动程序处理完中断后，它会通过对 SD 总线接口提供的中断确认例程的显式调用来通知总线驱动程序。 有关中断确认例程的详细信息，请参阅 [**PSDBUS \_ 确认 \_ INT \_ 例程**](/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_acknowledge_int_routine)。 当总线驱动程序收到此调用时，它会重新启用中断。

SD 设备驱动程序具有两个有关 IRQ 级别的选项， (其运行的 IRQLs) 。 SD 驱动程序可以独占方式在被动 \_ 级别运行，也可以 \_ 在中断通知回调例程的上下文中或在被动 \_ 级别的其他时间运行。 如果 SD 设备驱动程序以独占方式在被动 \_ 级别运行，则总线驱动程序会负责同步中断。 如果你的设备可以在不严格限制中断延迟的情况下运行，请选择此选项，因为它将简化你的驱动程序的设计。 除了将中断同步任务卸载到总线驱动程序外，还有其他好处。 例如，驱动程序必须经常传输数据以响应中断。 如果驱动程序的回调例程在被动级别运行 \_ ，则可以随意执行同步 i/o 操作，而不是异步操作。 如果回调例程在调度级别运行 \_ ，则在执行同步 i/o 之前，驱动程序必须等待，直到它在较低的 IRQL 下运行。

SD 设备驱动程序指定在初始化 SD bus 接口时，它将在其上运行的 IRQL。 若要在 \_ 中断通知回调例程中的调度级别运行，驱动程序必须将 [**SDBUS \_ 接口 \_ 参数**](/previous-versions/windows/hardware/drivers/ff537919(v=vs.85))结构的 **CallbackAtDpcLevel** 成员设置为 **TRUE** ，并将此结构传递给接口初始化例程。 有关接口例程的说明，请参阅 [**PSDBUS \_ INITIALIZE \_ interface \_ 例程**](/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)。 若要专门在被动 \_ 级别运行，驱动程序必须将 **CallbackAtDpcLevel** 设置为 **FALSE**。

 

