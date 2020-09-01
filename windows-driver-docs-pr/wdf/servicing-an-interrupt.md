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
ms.openlocfilehash: 2a803b272a2d5f5581c30365acd4835f9e7e6a3c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184263"
---
# <a name="servicing-an-interrupt"></a>为中断提供服务


本主题介绍如何为 DIRQL 中断服务。 有关维护被动级中断的信息，请参阅 [支持被动级别中断](supporting-passive-level-interrupts.md#servicing)。

为中断提供服务包括两个步骤：

1.  将可变信息 (例如，在以 IRQL = DIRQL 运行的中断服务例程中快速注册内容) 。

2.  在延迟的过程调用中处理已保存的可变信息 (DPC) ，以 IRQL = 调度 \_ 级别运行。

3.  如有必要，请在 IRQL = 被动级别执行额外的工作 \_ 。

当设备生成硬件中断时，框架会调用驱动程序的中断服务例程 (ISR) ，这是基于框架的驱动程序作为 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数实现的。

在设备的 DIRQL 上运行的 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数必须快速保存中断信息，如注册内容，如果发生其他中断，则会丢失该函数。

通常情况下， [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数计划 (DPC) 的延迟过程调用，以便在较低的 IRQL (调度级别) 处理保存的信息 \_ 。 基于框架的驱动程序将 DPC 例程作为 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 回调函数实现。

大多数驱动程序对每种类型的中断使用单个 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数。 若要计划*EvtInterruptDpc*回调函数的执行，驱动程序必须从[*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数中调用[**WdfInterruptQueueDpcForIsr**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr) 。

如果你的驱动程序为每个设备创建多个 [框架队列对象](framework-queue-objects.md) ，则可以考虑对每个队列使用单独的 [DPC 对象](/windows-hardware/drivers/ddi/wdfdpc/) 和 [*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 的回调函数。 若要计划 *EvtDpcFunc* 回调函数的执行，驱动程序必须首先通过调用 [**WdfDpcCreate**](/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpccreate)来创建一个或多个 DPC 对象，通常是在驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中。 然后，驱动程序的 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调函数可以调用 [**WdfDpcEnqueue**](/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpcenqueue)。

驱动程序通常会在其[*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数中[完成 i/o 请求](completing-i-o-requests.md)。

有时，驱动程序必须在 IRQL = 被动级别执行一些中断服务操作 \_ 。 在这种情况下，驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 回调函数（在 irql = 调度级别执行） \_ 可以计划执行一个或多个 [框架工作项，这些工作项](using-framework-work-items.md)在 irql = 被动 \_ 级别运行。

有关在服务设备中断时使用工作项的驱动程序的示例，请参阅 [PCIDRV](sample-kmdf-drivers.md) 示例驱动程序。

 

