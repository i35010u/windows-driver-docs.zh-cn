---
title: 启用和禁用中断
description: 启用和禁用中断
ms.assetid: 432907e7-05a3-4a99-a291-33bd1eefa94c
keywords:
- 硬件中断 WDK KMDF，启用
- 中断 WDK KMDF，启用
- 硬件中断 WDK KMDF，禁用
- 中断 WDK KMDF，禁用
- 状态信息 WDK KMDF，启用中断
- 状态信息 WDK KMDF，禁用中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1d12b9d225e1854953ad1ea385e89db493c939
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191747"
---
# <a name="enabling-and-disabling-interrupts"></a>启用和禁用中断


如果驱动程序处理设备中断，则它必须提供启用和禁用中断的 [*EvtInterruptEnable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable) 和 [*EvtInterruptDisable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable) 回调函数。 通常，这些回调函数在设备的 DIRQL 上运行，并且必须执行启用和禁用设备中断机制所需的任何操作。 对于 [被动级别中断](supporting-passive-level-interrupts.md)，这些回调函数以 IRQL = PASSIVE_LEVEL 运行，同时保持被动级中断锁。

如果你的驱动程序必须执行与启用或禁用中断相关的其他操作，并且如果无法在 IRQL = DIRQL 上执行这些附加操作，则驱动程序还可以提供 [*EvtDeviceD0EntryPostInterruptsEnabled*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled) 和 [*EvtDeviceD0ExitPreInterruptsDisabled*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled) 回调函数。 这两个回调函数在 IRQL = 被动 \_ 级别运行，不持有中断锁，并且可以调用在 IRQL = DIRQL 中不可用的框架对象方法。

每次设备进入工作 (D0) 状态时，框架都将调用驱动[*程序的*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) [*EvtInterruptEnable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)和[*EvtDeviceD0EntryPostInterruptsEnabled*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)回调函数。

在框架调用驱动程序的[*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调函数之前，每次设备离开其工作状态时，框架都会调用驱动程序的[*EvtDeviceD0ExitPreInterruptsDisabled*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)和[*EvtInterruptDisable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)回调函数。 有关框架何时调用驱动程序的回调函数的详细信息，请参阅 [PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

不得假设每次框架调用驱动程序的 [*EvtInterruptEnable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable) 回调函数时，设备都将使用相同的中断资源。 有时，PnP 管理器会重新 [分发系统资源](the-pnp-manager-redistributes-system-resources.md)，并且它可能会向设备分配新的中断资源。

驱动程序可以调用 [**WdfInterruptGetInfo**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptgetinfo) 来确定设备的中断资源。 驱动程序可以调用 [**WdfInterruptGetDevice**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptgetdevice) 来确定中断对象所属的设备。  (几个驱动程序可以调用 [**WdfInterruptWdmGetInterrupt**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptwdmgetinterrupt)。 ) 

若要直接启用和禁用中断，驱动程序可以调用中断对象的 [**WdfInterruptEnable**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptenable) 和 [**WdfInterruptDisable**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptdisable) 方法，该方法调用驱动程序的 [*EvtInterruptEnable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable) 和 [*EvtInterruptDisable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable) 事件回调函数。 但是，大多数驱动程序应该只允许框架在适当的时间调用 *EvtInterruptEnable* 和 *EvtInterruptDisable* 回调函数。

 

