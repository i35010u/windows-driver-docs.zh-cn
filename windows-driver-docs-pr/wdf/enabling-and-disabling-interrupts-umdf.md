---
title: 启用和禁用中断
description: 启用和禁用中断
ms.assetid: 52846461-4F08-4546-93F5-F2469C6E3AD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfe10c29c925970fb2efe36ef709229d7f164ae0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368733"
---
# <a name="enabling-and-disabling-interrupts"></a>启用和禁用中断


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果您的驱动程序处理设备中断，它必须提供[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)并[ *OnInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)回调函数启用和禁用中断。 这些回调函数必须执行会尽一切努力启用和禁用设备的中断机制。

如果您的驱动程序必须执行启用或禁用中断，该驱动程序还可以提供与相关的其他操作[ **IPnpCallbackHardwareInterrupt::OnD0EntryPostInterruptsEnabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled)并[ **IPnpCallbackHardwareInterrupt::OnD0ExitPreInterruptsDisabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled)回调函数。

框架将调用的驱动程序[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)并[ **IPnpCallbackHardwareInterrupt::OnD0EntryPostInterruptsEnabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0entrypostinterruptsenabled)回调函数每次设备进入其工作 (D0) 状态，该框架已调用驱动程序的后[ **OnD0Entry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)回调函数。 框架将调用的驱动程序[ **IPnpCallbackHardwareInterrupt::OnD0ExitPreInterruptsDisabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardwareinterrupt-ond0exitpreinterruptsdisabled)并[ *OnInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)回调函数设备使其工作状态之前框架将调用驱动程序的, 每次[ **OnD0Exit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)回调函数。 当框架将调用驱动程序的回调函数的详细信息，请参阅[基于 UMDF 驱动程序中的 PnP 和电源管理](pnp-and-power-management-in-umdf-drivers.md)。

您必须假定框架将调用您的驱动程序的每次设备将使用相同的中断资源[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)回调函数。 有时 PnP 管理器将重新分发的系统资源，并且它可能会将新 interrupt 资源分配给你的设备。

该驱动程序可以调用[ **IWDFInterrupt::GetInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-getinfo)来确定设备的中断资源。 该驱动程序可以调用[ **IWDFInterrupt::GetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-getdevice)来确定中断对象所属的设备。

若要启用和禁用中断直接，驱动程序可以调用中断对象[ **IWDFInterrupt::Enable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-enable)并[ **IWDFInterrupt::Disable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-disable)方法，调用的驱动程序[ *OnInterruptEnable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)并[ *OnInterruptDisable* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)事件回调函数。 但是，大多数驱动程序只应允许 framework 来调用*OnInterruptEnable*并*OnInterruptDisable*在适当时间的回调函数。

 

 





