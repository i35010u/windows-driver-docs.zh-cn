---
title: 为中断提供服务
description: 为中断提供服务
ms.assetid: b6306d2c-a7be-4fc3-8123-4d2b5c60c988
keywords:
- 硬件中断 WDK KMDF，维护服务
- 中断 WDK KMDF，维护服务
- 服务中断 WDK KMDF
- 中断服务例程 WDK KMDF
- Isr WDK KMDF
- 延迟的过程调用 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c265a458ca8a852b67fd4452c86f25a23fa3963
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376187"
---
# <a name="servicing-an-interrupt"></a>为中断提供服务


本主题介绍如何以服务的 DIRQL 中断。 有关维护服务的被动级别中断的信息，请参阅[支持被动中断级别](supporting-passive-level-interrupts.md#servicing)。

服务中断包括两个，并有时三个步骤：

1.  快速保存易失性信息 （如寄存器内容），在中断服务例程运行在 IRQL = DIRQL。

2.  处理延迟的过程调用 (DPC) 的 IRQL 运行中已保存的易失性信息 = 调度\_级别。

3.  执行额外的工作在 IRQL = 被动\_级别，如有必要。

当设备生成的硬件中断时，框架将调用驱动程序的中断服务例程 (ISR) 作为实现的基于框架的驱动程序[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数。

[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数，如设备的 DIRQL，快速保存中断的信息，必须在运行注册的内容，将会丢失，如果另一个中断发生的。

通常情况下， [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数计划延迟的过程调用 (DPC) 来处理更高版本在较低的 IRQL 已保存的信息 (调度\_级别)。 基于框架的驱动程序实现为 DPC 例程[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数。

大多数驱动程序使用单个[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)中断每种类型的回调函数。 若要计划的执行*EvtInterruptDpc*驱动程序必须调用回调函数[ **WdfInterruptQueueDpcForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)中[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数。

如果您的驱动程序创建多个[framework 队列对象](framework-queue-objects.md)对于每个设备，你可以考虑使用单独[DPC 对象](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/)并[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)每个队列的回调函数。 若要计划的执行*EvtDpcFunc*回调函数，该驱动程序必须先创建一个或多个 DPC 对象通过调用[ **WdfDpcCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpccreate)，通常在驱动程序[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 然后，驱动程序的[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数可以调用[ **WdfDpcEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpcenqueue)。

驱动程序通常[完成 I/O 请求](completing-i-o-requests.md)在其[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或者[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数。

有时一个驱动程序必须一些中断服务在执行操作的 IRQL = 被动\_级别。 在此类情况下，驱动程序的[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数，执行在 IRQL = 调度\_级别，可以安排执行的一个或多个[framework 工作项](using-framework-work-items.md)，它运行在 IRQL = 被动\_级别。

有关使用服务设备中断时工作项的驱动程序示例，请参阅[PCIDRV](sample-kmdf-drivers.md)示例驱动程序。

 

 





