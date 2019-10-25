---
title: 启用和禁用中断
description: 启用和禁用中断
ms.assetid: 52846461-4F08-4546-93F5-F2469C6E3AD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 692b8c2e6289eac7d9aca8fa401317fbccf635c7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838004"
---
# <a name="enabling-and-disabling-interrupts"></a>启用和禁用中断


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果驱动程序处理设备中断，则它必须提供启用和禁用中断的[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)和[*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)回调函数。 这些回调函数必须执行启用和禁用设备中断机制所需的任何操作。

如果驱动程序必须执行与启用或禁用中断相关的其他操作，则驱动程序还可以提供[**IPnpCallbackHardwareInterrupt：： OnD0EntryPostInterruptsEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled)和[**IPnpCallbackHardwareInterrupt：： OnD0ExitPreInterruptsDisabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled)回调函数。

每次设备进入其工作（D0）状态时，框架都调用驱动程序的[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)和[**IPnpCallbackHardwareInterrupt：： OnD0EntryPostInterruptsEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled)回调函数。[**OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)回调函数。 每次设备离开其工作状态时，框架都会调用驱动程序的[**IPnpCallbackHardwareInterrupt：： OnD0ExitPreInterruptsDisabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled)和[*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)回调函数，然后框架会调用驱动程序的[**OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)回调函数。 有关框架何时调用驱动程序的回调函数的详细信息，请参阅[基于 UMDF 的驱动程序中的 PnP 和电源管理](pnp-and-power-management-in-umdf-drivers.md)。

不得假设每次框架调用驱动程序的[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)回调函数时，设备都将使用相同的中断资源。 有时，PnP 管理器会重新分发系统资源，并且它可能会向设备分配新的中断资源。

驱动程序可以调用[**IWDFInterrupt：： GetInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-getinfo)来确定设备的中断资源。 驱动程序可以调用[**IWDFInterrupt：： GetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-getdevice)来确定中断对象所属的设备。

若要直接启用和禁用中断，驱动程序可以调用中断对象的[**IWDFInterrupt：： enable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-enable)和[**IWDFInterrupt：:D i)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-disable)方法，该方法调用驱动程序的[*OnInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)和[*OnInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)事件回调函数。 但是，大多数驱动程序应该只允许框架在适当的时间调用*OnInterruptEnable*和*OnInterruptDisable*回调函数。

 

 





