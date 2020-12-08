---
title: 启用和禁用 (UMDF 1) 的中断
description: 启用和禁用中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4e04f54664eb415cc3efcdc749d8fad03c25ce1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815773"
---
# <a name="enabling-and-disabling-interrupts-umdf-1"></a>启用和禁用 (UMDF 1) 的中断


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果驱动程序处理设备中断，则它必须提供启用和禁用中断的 [*OnInterruptEnable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable) 和 [*OnInterruptDisable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable) 回调函数。 这些回调函数必须执行启用和禁用设备中断机制所需的任何操作。

如果驱动程序必须执行与启用或禁用中断相关的其他操作，则驱动程序还可以提供 [**IPnpCallbackHardwareInterrupt：： OnD0EntryPostInterruptsEnabled**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled) 和 [**IPnpCallbackHardwareInterrupt：： OnD0ExitPreInterruptsDisabled**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled) 回调函数。

每当设备进入工作 (D0) 状态时，框架都将调用驱动 [**程序的**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) [*OnInterruptEnable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)和 [**IPnpCallbackHardwareInterrupt：： OnD0EntryPostInterruptsEnabled**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled)回调函数。 在框架调用驱动程序的 [**OnD0Exit**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)回调函数之前，每次设备离开其工作状态时，框架都会调用驱动程序的 [**IPnpCallbackHardwareInterrupt：： OnD0ExitPreInterruptsDisabled**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled)和 [*OnInterruptDisable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)回调函数。 有关框架何时调用驱动程序的回调函数的详细信息，请参阅 [基于 UMDF 的驱动程序中的 PnP 和电源管理](pnp-and-power-management-in-umdf-drivers.md)。

不得假设每次框架调用驱动程序的 [*OnInterruptEnable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable) 回调函数时，设备都将使用相同的中断资源。 有时，PnP 管理器会重新分发系统资源，并且它可能会向设备分配新的中断资源。

驱动程序可以调用 [**IWDFInterrupt：： GetInfo**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-getinfo) 来确定设备的中断资源。 驱动程序可以调用 [**IWDFInterrupt：： GetDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-getdevice) 来确定中断对象所属的设备。

若要直接启用和禁用中断，驱动程序可以调用中断对象的 [**IWDFInterrupt：： enable**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-enable) 和 [**IWDFInterrupt：:D i)**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-disable) 方法，该方法调用驱动程序的 [*OnInterruptEnable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable) 和 [*OnInterruptDisable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable) 事件回调函数。 但是，大多数驱动程序应该只允许框架在适当的时间调用 *OnInterruptEnable* 和 *OnInterruptDisable* 回调函数。

 

