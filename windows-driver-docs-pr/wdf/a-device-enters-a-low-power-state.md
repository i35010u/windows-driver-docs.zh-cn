---
title: 设备进入低功耗状态
description: 了解设备进入低功耗状态时将发生的情况。 例如，当设备处于空闲状态时，系统仍处于正常工作状态。
ms.assetid: 07d7c460-4316-40a9-b502-f7c1bd1182c2
keywords:
- 电源管理 WDK KMDF、低功耗状态
- 低功耗状态 WDK KMDF
- 电源状态 WDK KMDF
- 设备电源状态 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 空闲的关闭 WDK KMDF
- 电源管理 WDK KMDF、空闲关机
- 系统睡眠状态 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2d85a90fce4de7b289af43205e588aa783d2c03
ms.sourcegitcommit: 2aedb606f9f14e74687f0d3da60e14fc6ffffa7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91544426"
---
# <a name="a-device-enters-a-low-power-state"></a>设备进入低功耗状态


如果发生以下情况之一，设备会将其工作 (D0) 状态，并进入低功耗状态：

-   设备处于空闲状态 (也就是说，没有) 访问它，并且能够进入低功耗空闲状态，而系统仍处于正常工作 (S0) 状态。

-   系统的电源状态已从其工作 (S0) 状态更改为低功耗状态。  (驱动程序可以调用 [**WdfDeviceGetSystemPowerAction**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetsystempoweraction) 来确定系统电源状态更改的原因。 ) 

对于支持设备的每个函数和筛选器驱动程序，框架按顺序执行以下操作，一次一个驱动程序，从驱动程序堆栈最高的驱动程序开始：

1.  如果驱动程序使用的是自管理 i/o，则框架将调用驱动程序的 [*EvtDeviceSelfManagedIoSuspend*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend) 回调函数。

2.  框架将停止驱动程序的所有电源管理 i/o 队列，并在)  (它们的 [*EvtIoStop*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop) 回调函数。

3.  如果驱动程序是设备的电源策略所有者，则框架将调用其 [*EvtDeviceArmWakeFromS0*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)、 [*EvtDeviceArmWakeFromSx*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)或 [*EvtDeviceArmWakeFromSxWithReason*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx_with_reason) 回调函数。

4.  如果硬件和驱动程序支持 DMA，则框架将调用驱动程序的 [*EvtDmaEnablerSelfManagedIoStop*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_selfmanaged_io_stop)、 [*EvtDmaEnablerFlush*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_flush)和 [*EvtDmaEnablerDisable*](/windows-hardware/drivers/ddi/wdfdmaenabler/nc-wdfdmaenabler-evt_wdf_dma_enabler_disable) 回调函数 (如果它们) 为创建的每个 DMA 通道。

5.  如果) 存在驱动程序 (，则框架将调用该驱动程序的 [*EvtDeviceD0ExitPreInterruptsDisabled*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled) 回调函数，然后调用驱动程序的 [*EvtInterruptDisable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable) 回调函数 (（如果它存在于每个中断) ），以便驱动程序可以禁用设备中断。

6.  如果) 存在驱动程序 (，则框架将调用该驱动程序的 [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 回调函数。

总线驱动程序是堆栈中最后一个调用的驱动程序。 当框架调用总线驱动程序的 [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 回调函数时，回调函数会将设备的电源状态设置 (总线) 的子设备设置为低功耗状态。 此框架指定 D3 低功耗状态，除非电源策略所有者指定了不同的低功耗状态。

 

