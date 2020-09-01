---
title: 设备专用的线程
description: 设备专用的线程
ms.assetid: 2e11e2c9-aefd-4b7b-8d80-7eb1da9f7cce
keywords:
- 线程对象 WDK 内核
- 设备专用线程 WDK 内核
- 运行时优先级倒置 WDK 内核
- PsCreateSystemThread
- KeSetBasePriorityThread
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 399fa55640e45cf644ac8650613a909417b82ee1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191931"
---
# <a name="device-dedicated-threads"></a>设备专用的线程





很少使用 (如软盘控制器) 的设备或设备的驱动程序可以通过创建一个设备专用系统线程来解决许多 "正在等待" 的问题。 此外，大多数文件系统驱动程序都使用系统工作线程并提供工作线程回调例程。

如果设备驱动程序具有其自己的线程上下文，或在系统线程上下文中运行，则设备专用线程或顶级驱动程序的工作线程回调例程可以在驱动程序的设备扩展的共享通信区域中同步对调度程序对象（如 [事件对象](event-objects.md) 或 [信号量对象](semaphore-objects.md)）的操作。 例如，设备专用线程可以等待共享的调度程序对象，而不使用线程的设备，方法是调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 作为信号量。 在调用设备驱动程序以执行 i/o 操作之前 (此时，它会将信号量设置为终止状态) ，其等待线程将不使用 CPU 时间。

驱动程序可以调用 [**PsCreateSystemThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread) 来创建驱动程序或设备专用线程，然后调用 [**KeSetBasePriorityThread**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kesetbaseprioritythread) 来设置线程的基本优先级。 驱动程序应指定一个可避免在 SMP 计算机中 *运行时优先级倒置* 的优先级值。 也就是说，如果将驱动程序创建的线程的基本优先级设置得过高，则可能会在执行提交该驱动程序的 i/o 请求的低优先级线程时产生延迟。

由于线程对象本身就是一种类型的调度程序对象，因此线程可以等待另一个线程完成。 若要获取与线程关联的线程对象指针，驱动程序可以调用 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)，传入从 **PsCreateSystemThread**接收的线程句柄。

线程可以调用 [**KeDelayExecutionThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread) 来等待可能为完整时间段或更长时间段的间隔。 **KeDelayExecutionThread**间隔的粒度约为10毫秒。 由于 **KeDelayExecutionThread** 是计时器驱动例程，因此，其间隔的粒度稍快或慢于10毫秒，具体取决于平台。

 

