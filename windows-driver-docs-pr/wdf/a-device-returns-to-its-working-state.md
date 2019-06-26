---
title: 设备回到工作状态
description: 设备回到工作状态
ms.assetid: 0a5bdaf5-ed9e-44d0-bc8a-876ceb342520
keywords:
- 设备电源状态 WDK KMDF
- 工作状态 WDK KMDF
- 电源状态 WDK KMDF
- 系统唤醒 WDK KMDF
- 电源管理 WDK KMDF，唤醒功能
- 唤醒功能 WDK KMDF
- 睡眠电源管理 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54ecf5c3a87225e313f33e13d2bea1128cd9e765
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385332"
---
# <a name="a-device-returns-to-its-working-state"></a>设备回到工作状态


如果发生下列其中一项处于低功耗状态的设备将恢复工作状态：

-   设备检测到的外部事件，并触发其总线上的唤醒信号。 检测到唤醒信号调用总线驱动程序[ **WdfDeviceIndicateWakeStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceindicatewakestatus)。 因此，框架将调用总线驱动程序[ *EvtDeviceDisableWakeAtBus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_disable_wake_at_bus)回调函数。

-   设备处于空闲状态，并将驱动程序调用[ **WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)。

-   系统的电源状态已从低功耗状态更改为其工作 (S0) 状态。

在每种情况下，框架将调用总线驱动程序[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数，然后将设备 （在总线的子设备） 还原到其工作 (D0) 状态。

对于每个函数和筛选器驱动程序支持设备，该框架执行以下操作，在序列中，使用驱动程序的最低驱动程序堆栈中启动一个时，驱动程序：

1.  框架将调用的驱动程序[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数 （如果存在）。

2.  框架将调用的驱动程序[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)回调函数 （如果存在） 为每个中断，然后它调用的驱动程序[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)回调函数 （如果存在），以便该驱动程序可以启用设备中断。

3.  如果硬件和驱动程序支持 DMA，框架将调用的驱动程序[ *EvtDmaEnablerFill*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_fill)， [ *EvtDmaEnablerEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_enable)，和[ *EvtDmaEnablerSelfManagedIoStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_start)回调函数 （如果存在） 用于创建每个 DMA 通道。

4.  如果该驱动程序是设备的电源策略所有者，框架将调用其[ *EvtDeviceDisarmWakeFromS0* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)或[ *EvtDeviceDisarmWakeFromSx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)回调函数。

5.  框架将调用的驱动程序[ *EvtChildListScanForChildren* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)回调函数 （如果存在）。

6.  Framework 重新启动所有驱动程序的电源管理的 I/O 队列并调用其[ *EvtIoResume* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)回调函数 （如有必要）。

7.  如果该驱动程序使用的自托管的 I/O，框架将调用的驱动程序[ *EvtDeviceSelfManagedIoRestart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_restart)回调函数。

 

 





