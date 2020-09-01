---
title: 移植中断
description: 移植中断
ms.assetid: E91B971D-044C-45A4-AD76-44AFB1213F8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f34b17da37c893c4482170355a979d9f101009c3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191731"
---
# <a name="porting-interrupts"></a>移植中断


支持和维护中断的代码在 WDF 和 WDM 驱动程序中是类似的。 主要区别在于：

-   WDF 驱动程序通过从其[*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调调用[**WDFINTERRUPTCREATE**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) ，创建 WDFINTERRUPT 对象并将其中断服务例程注册 (ISR) 回调。
-   WDM 驱动程序创建 KINTERRUPT 结构，并在 [**IRP \_ MN \_ 开始 \_ 设备**](../kernel/irp-mn-start-device.md) 处理期间连接该结构。

WDF 驱动程序中的 [*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) 回调执行与 WDM 驱动程序的 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 例程相同的任务。 *EvtInterruptIsr*回调调用[**WdfInterruptQueueDpcForIsr**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)将[*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调排队，以便以后在调度级别进行处理 \_ 。 在响应中，框架将一个 DPC 对象添加到运行此回调的系统队列。

有关框架中断对象的详细信息，请参阅 [处理硬件中断](handling-hardware-interrupts.md)。

 

