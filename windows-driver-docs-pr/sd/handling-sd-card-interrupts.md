---
title: 处理 SD 卡中断
description: 处理 SD 卡中断
ms.assetid: 40c18af4-6b23-4893-b82f-7fe652929069
keywords:
- SD WDK 总线中断
- 中断 WDK SD 总线
- 于 Irql WDK SD 总线
- 硬件中断 WDK SD 总线
- 中断通知 WDK SD 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6acf19daa493a712d31474b31092d11bce3f0c46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342870"
---
# <a name="handling-sd-card-interrupts"></a>处理 SD 卡中断


安全数字 (SD) 卡驱动程序没有中断服务例程 (Isr)，它们没有获取中断请求 (IRQ) 资源。 SD 总线驱动程序检测到并截获硬件中断，然后报告这些设备驱动程序通过中断通知回调例程[ **PSDBUS\_回调\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff537617)部分中所述， [Secure Digital (SD) 驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/ff537964)并[打开并初始化 SD 总线接口](https://msdn.microsoft.com/library/windows/hardware/ff537442)。

设备驱动程序无需完成处理中断通知回调例程的上下文中的中断。 该驱动程序可以从回调例程返回并完成其自身的上下文中的中断处理。 完成该驱动程序处理中断后，它会通过对与 SD 总线接口提供一个中断确认例程的显式调用通知总线驱动程序。 有关中断确认例程的详细信息，请参阅[ **PSDBUS\_确认\_INT\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff537616)。 当总线驱动程序收到此调用时，它将重新启用中断。

SD 设备驱动程序可以从了它们的运行与的 IRQ 级别 (于 Irql) 相关的两个选项。 SD 驱动程序可以运行以独占方式在被动\_级别，或者它可以运行在调度\_级别时在上下文中的中断通知回调例程而在被动\_级别余下的时间。 SD 设备驱动程序以独占方式在被动的运行时\_级别，总线驱动程序假定负责同步中断。 如果你的设备可以运行不受中断延迟严格限制，因为这将简化您的驱动程序的设计，请选择此选项。 除了卸载中断同步总线驱动程序上的任务，还有其他好处。 例如，驱动程序必须频繁地传输到中断的响应中的数据。 如果在被动运行驱动程序的回调例程\_级别，它可免费执行同步 I/O 操作而不是一个异步操作。 如果在调度运行回调例程\_级别，该驱动程序必须等待，直到在较低的 IRQL 运行之前执行同步 I/O。

SD 设备驱动程序指定的运行时初始化 SD 总线接口 IRQL。 若要运行在调度\_级别在中断通知回调例程，该驱动程序必须设置**CallbackAtDpcLevel**的成员[ **SDBUS\_接口\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff537919)结构**TRUE**并将此结构传递给接口初始化例程。 接口例程的说明，请参阅[ **PSDBUS\_初始化\_接口\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff537618)。 若要运行以独占方式在被动\_级别，该驱动程序必须设置**CallbackAtDpcLevel**到**FALSE**。

 

 




