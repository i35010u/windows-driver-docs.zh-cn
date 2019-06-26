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
ms.openlocfilehash: 97475d631dbb907376886052fa8ea1fb564717f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385009"
---
# <a name="device-dedicated-threads"></a>设备专用的线程





通过创建设备专用系统线程，慢速设备或很少使用 （如软盘控制器） 的设备的驱动程序来解决许多"等待"问题。 此外，大多数文件系统驱动程序使用系统工作线程数，并提供工作线程回调例程。

如果设备驱动程序具有其自己的线程上下文，或在系统线程上下文中运行，设备专用线程或最高级别的驱动程序的工作线程回调例程可以同步操作调度程序对象，如[事件对象](event-objects.md)或[信号量对象](semaphore-objects.md)，驱动程序的设备扩展共享的通信区域中。 例如，设备专用线程可以等待共享调度程序对象，而线程的设备不在使用中，通过调用[ **KeWaitForSingleObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)信号量。 设备驱动程序调用以执行 I/O 操作 （此时它将信号量为用信号通知状态），直到其等待线程使用任何 CPU 时间。

驱动程序可以调用[ **PsCreateSystemThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)以创建驱动程序或设备专用线程，然后调用[ **KeSetBasePriorityThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kesetbaseprioritythread)来设置线程的基本优先级。 该驱动程序应指定一个优先级值，可避免*运行时优先级倒置*SMP 计算机中。 即，将设置过高的驱动程序创建线程的基本优先级会创建延迟中提交该驱动程序的 I/O 请求的较低优先级线程的执行。

由于线程对象本身的调度程序对象类型，一个线程可以等待另一个线程完成。 若要获取与线程相关联的线程对象指针，驱动程序可以调用[ **ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)，并传入从接收到的线程句柄**PsCreateSystemThread**.

一个线程可以调用[ **KeDelayExecutionThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kedelayexecutionthread)等待可能是一个完整时间段的时间间隔或更长时间。 粒度**KeDelayExecutionThread**间隔为大约 10 毫秒。 因为**KeDelayExecutionThread**是计时器驱动的例程，间隔的时间长度的粒度是略有更快或低于 10 毫秒，具体取决于平台。

 

 




