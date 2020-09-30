---
title: 设备回到工作状态
description: 了解设备返回到其工作状态时会发生什么情况。 例如，当外部事件触发唤醒信号时。
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
ms.openlocfilehash: d9ac9f42171fd70cd7c7e71bee135beb1c541527
ms.sourcegitcommit: 2aedb606f9f14e74687f0d3da60e14fc6ffffa7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91544394"
---
# <a name="a-device-returns-to-its-working-state"></a>设备回到工作状态


如果发生以下情况之一，则处于低功耗状态的设备将恢复为其工作状态：

-   设备检测到外部事件，并在其总线上触发唤醒信号。 检测唤醒信号的总线驱动程序调用 [**WdfDeviceIndicateWakeStatus**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus)。 因此，框架将调用总线驱动程序的 [*EvtDeviceDisableWakeAtBus*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus) 回调函数。

-   设备处于空闲状态，驱动程序调用 [**WdfDeviceStopIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)。

-   系统的电源状态已从低功耗状态更改为其工作 (S0) 状态。

在上述每种情况下，框架都会调用总线驱动程序的 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调函数，该函数随后会将) 总线的子设备 (设备还原到其工作 (D0) 状态。

对于支持设备的每个函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈中的最低驱动程序开始：

1.  如果) 存在驱动程序 (，则框架将调用该驱动程序的 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调函数。

2.  如果) 对于每个中断，框架将调用驱动程序的 [*EvtInterruptEnable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable) 回调函数 (，然后它将调用驱动程序的 [*EvtDeviceD0EntryPostInterruptsEnabled*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled) 回调函数 (如果它存在) ，以便驱动程序可以启用设备中断。

3.  如果硬件和驱动程序支持 DMA，则框架将调用驱动程序的 [*EvtDmaEnablerFill*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)、 [*EvtDmaEnablerEnable*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)和 [*EvtDmaEnablerSelfManagedIoStart*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start) 回调函数 (如果它们) 为创建的每个 DMA 通道存在，则为。

4.  如果驱动程序是设备的电源策略所有者，则框架将调用其 [*EvtDeviceDisarmWakeFromS0*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0) 或 [*EvtDeviceDisarmWakeFromSx*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx) 回调函数。

5.  如果) 存在驱动程序 (，则框架将调用该驱动程序的 [*EvtChildListScanForChildren*](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children) 回调函数。

6.  框架将重新启动所有驱动程序的电源管理 i/o 队列，并在必要)  (调用其 [*EvtIoResume*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume) 回调函数。

7.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的 [*EvtDeviceSelfManagedIoRestart*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart) 回调函数。

 

