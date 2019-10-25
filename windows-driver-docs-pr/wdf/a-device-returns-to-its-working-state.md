---
title: 设备回到工作状态
description: 设备回到工作状态
ms.assetid: 0a5bdaf5-ed9e-44d0-bc8a-876ceb342520
keywords:
- 设备电源状态 WDK KMDF
- 工作状态 WDK KMDF
- 电源状态 WDK KMDF
- 系统唤醒 KMDF
- 电源管理 WDK KMDF、唤醒功能
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf921a1fb8c8d2c1857563979496467788497e4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843654"
---
# <a name="a-device-returns-to-its-working-state"></a>设备回到工作状态


如果发生以下情况之一，则处于低功耗状态的设备将恢复为其工作状态：

-   设备检测到外部事件，并在其总线上触发唤醒信号。 检测唤醒信号的总线驱动程序调用[**WdfDeviceIndicateWakeStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus)。 因此，框架将调用总线驱动程序的[*EvtDeviceDisableWakeAtBus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)回调函数。

-   设备处于空闲状态，驱动程序调用[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)。

-   系统的电源状态已从低功耗状态更改为工作（S0）状态。

在上述每种情况下，框架都会调用总线驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数，该函数随后将设备（总线的子设备）还原到其工作（D0）状态。

对于支持设备的每个函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈中的最低驱动程序开始：

1.  框架调用驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数（如果存在）。

2.  框架为每个中断调用驱动程序的[*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)回调函数（如果存在），然后调用驱动程序的[*EvtDeviceD0EntryPostInterruptsEnabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)回调函数（如果存在），以便驱动程序可以启用设备中断。

3.  如果硬件和驱动程序支持 DMA，框架会为创建的每个 DMA 通道调用驱动程序的[*EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [*EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)和[*EvtDmaEnablerSelfManagedIoStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)回调函数（如果存在）。

4.  如果驱动程序是设备的电源策略所有者，则框架将调用其[*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)或[*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)回调函数。

5.  框架调用驱动程序的[*EvtChildListScanForChildren*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)回调函数（如果存在）。

6.  框架将重新启动所有驱动程序的电源管理 i/o 队列，并调用其[*EvtIoResume*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)回调函数（如有必要）。

7.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的[*EvtDeviceSelfManagedIoRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)回调函数。

 

 





