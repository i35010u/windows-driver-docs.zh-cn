---
title: 启用和禁用中断
description: 启用和禁用中断
ms.assetid: 432907e7-05a3-4a99-a291-33bd1eefa94c
keywords:
- WDK KMDF，启用的硬件中断
- 中断 WDK KMDF，启用
- 硬件中断 WDK KMDF，禁用
- 中断 WDK KMDF，禁用
- WDK KMDF，启用的状态信息会中断
- WDK KMDF，禁用的状态信息会中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57da85c8607baf9f0fd429f1f13c552a8456d0e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368727"
---
# <a name="enabling-and-disabling-interrupts"></a>启用和禁用中断


如果您的驱动程序处理设备中断，它必须提供[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)并[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)回调启用和禁用中断的函数。 通常情况下，这些回调函数运行设备的 DIRQL，并且必须执行会尽一切努力启用和禁用设备的中断机制。 有关[被动等级中断](supporting-passive-level-interrupts.md)，在 IRQL 运行这些回调函数时保留了被动级别中断锁定 = passive_level 调用。

如果您的驱动程序必须执行启用或禁用中断，与相关的其他操作和这些额外的操作无法执行在 IRQL = DIRQL，驱动程序还可以提供[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)并[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)回调函数。 这两个回调函数运行在 IRQL = 被动\_级别有一种无中断锁保留，并且可以调用框架在 IRQL 不可用的对象方法 = DIRQL。

框架将调用的驱动程序[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)并[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry_post_interrupts_enabled)回调函数每次在设备进入其工作 (D0) 状态，框架已调用驱动程序的后[ *EvtDeviceD0Entry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调函数。

框架将调用的驱动程序[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit_pre_interrupts_disabled)并[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)回调函数框架将调用的驱动程序之前，设备离开其工作状态，每次[ *EvtDeviceD0Exit* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)回调函数。 当框架将调用驱动程序的回调函数的详细信息，请参阅[PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

您必须假定框架将调用您的驱动程序的每次设备将使用相同的中断资源[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)回调函数。 有时 PnP 管理器[将重新分发的系统资源](the-pnp-manager-redistributes-system-resources.md)，并且它可能会将新 interrupt 资源分配给你的设备。

该驱动程序可以调用[ **WdfInterruptGetInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptgetinfo)来确定设备的中断资源。 该驱动程序可以调用[ **WdfInterruptGetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptgetdevice)来确定中断对象所属的设备。 (一些驱动程序可能会调用[ **WdfInterruptWdmGetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptwdmgetinterrupt)。)

若要启用和禁用中断直接，驱动程序可以调用中断对象[ **WdfInterruptEnable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptenable)并[ **WdfInterruptDisable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptdisable)方法，调用的驱动程序[ *EvtInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)并[ *EvtInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)事件回调函数。 但是，大多数驱动程序只应允许 framework 来调用*EvtInterruptEnable*并*EvtInterruptDisable*在适当时间的回调函数。

 

 





