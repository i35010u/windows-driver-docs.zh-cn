---
title: 处理 SD 卡中断
description: 处理 SD 卡中断
ms.assetid: 40c18af4-6b23-4893-b82f-7fe652929069
keywords:
- SD WDK 总线，中断
- 中断 WDK SD 总线
- IRQLs WDK SD 总线
- 硬件中断 WDK SD 总线
- 中断通知 WDK SD 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 299761d9bd1ed76b8719f98554d8616e6346fdc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844486"
---
# <a name="handling-sd-card-interrupts"></a>处理 SD 卡中断


安全数字（SD）卡驱动程序没有中断服务例程（Isr），并且它们不获取中断请求（IRQ）资源。 SD bus 驱动程序检测并截获硬件中断，然后通过中断通知回调例程[**PSDBUS\_回调\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-sdbus_callback_routine)将它们报告给设备驱动程序，如[安全数字部分（SD）驱动程序堆栈](https://docs.microsoft.com/windows-hardware/drivers/sd/sd-card-driver-stack)，并[打开和初始化 SD Bus 接口](https://docs.microsoft.com/windows-hardware/drivers/sd/opening--initializing-and-closing-an-sd-card-bus-interface)。

设备驱动程序无需在中断通知回调例程的上下文中完成中断处理。 驱动程序可以从回调例程返回并在其自身的上下文中完成中断处理。 当驱动程序处理完中断后，它会通过对 SD 总线接口提供的中断确认例程的显式调用来通知总线驱动程序。 有关中断确认例程的详细信息，请参阅[**PSDBUS\_确认\_INT\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_acknowledge_int_routine)。 当总线驱动程序收到此调用时，它会重新启用中断。

SD 设备驱动程序在其运行时具有两个有关 IRQ 级别（IRQLs）的选项。 SD 驱动程序可以独占方式在被动\_级别运行，也可以在中断通知回调例程的上下文中和被动\_级别的其他时间，在调度\_级别运行。 如果 SD 设备驱动程序以独占方式\_级别运行，则总线驱动程序会负责同步中断。 如果你的设备可以在不严格限制中断延迟的情况下运行，请选择此选项，因为它将简化你的驱动程序的设计。 除了将中断同步任务卸载到总线驱动程序外，还有其他好处。 例如，驱动程序必须经常传输数据以响应中断。 如果驱动程序的回调例程在被动\_级别运行，则可以随意执行同步 i/o 操作，而不是异步操作。 如果回调例程在调度\_级别运行，则在执行同步 i/o 之前，驱动程序必须等待，直到它在较低的 IRQL 下运行。

SD 设备驱动程序指定在初始化 SD bus 接口时，它将在其上运行的 IRQL。 若要在中断通知回调例程中的调度\_级别运行，驱动程序必须将[**SDBUS\_\_接口**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537919(v=vs.85))的**CallbackAtDpcLevel**成员设置为**TRUE** ，并将此结构传递给接口初始化例程。 有关 interface 例程的说明，请参阅[**PSDBUS\_INITIALIZE\_interface\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-psdbus_initialize_interface_routine)。 若要专门在被动\_级别运行，驱动程序必须将**CallbackAtDpcLevel**设置为**FALSE**。

 

 




