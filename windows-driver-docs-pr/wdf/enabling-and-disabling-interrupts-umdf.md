---
title: 启用和禁用中断
description: 启用和禁用中断
ms.assetid: 52846461-4F08-4546-93F5-F2469C6E3AD8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02834e52849b93c4f9cbb0c2966d4c69321e6ab2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567011"
---
# <a name="enabling-and-disabling-interrupts"></a>启用和禁用中断


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果您的驱动程序处理设备中断，它必须提供[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)并[ *OnInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/hh463895)回调函数启用和禁用中断。 这些回调函数必须执行会尽一切努力启用和禁用设备的中断机制。

如果您的驱动程序必须执行启用或禁用中断，该驱动程序还可以提供与相关的其他操作[ **IPnpCallbackHardwareInterrupt::OnD0EntryPostInterruptsEnabled** ](https://msdn.microsoft.com/library/windows/hardware/hh439750)并[ **IPnpCallbackHardwareInterrupt::OnD0ExitPreInterruptsDisabled** ](https://msdn.microsoft.com/library/windows/hardware/hh439755)回调函数。

框架将调用的驱动程序[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)并[ **IPnpCallbackHardwareInterrupt::OnD0EntryPostInterruptsEnabled** ](https://msdn.microsoft.com/library/windows/hardware/hh439750)回调函数每次设备进入其工作 (D0) 状态，该框架已调用驱动程序的后[ **OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)回调函数。 框架将调用的驱动程序[ **IPnpCallbackHardwareInterrupt::OnD0ExitPreInterruptsDisabled** ](https://msdn.microsoft.com/library/windows/hardware/hh439755)并[ *OnInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/hh463895)回调函数设备使其工作状态之前框架将调用驱动程序的, 每次[ **OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803)回调函数。 当框架将调用驱动程序的回调函数的详细信息，请参阅[基于 UMDF 驱动程序中的 PnP 和电源管理](pnp-and-power-management-in-umdf-drivers.md)。

您必须假定框架将调用您的驱动程序的每次设备将使用相同的中断资源[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)回调函数。 有时 PnP 管理器将重新分发的系统资源，并且它可能会将新 interrupt 资源分配给你的设备。

该驱动程序可以调用[ **IWDFInterrupt::GetInfo** ](https://msdn.microsoft.com/library/windows/hardware/hh451309)来确定设备的中断资源。 该驱动程序可以调用[ **IWDFInterrupt::GetDevice** ](https://msdn.microsoft.com/library/windows/hardware/hh451305)来确定中断对象所属的设备。

若要启用和禁用中断直接，驱动程序可以调用中断对象[ **IWDFInterrupt::Enable** ](https://msdn.microsoft.com/library/windows/hardware/hh451300)并[ **IWDFInterrupt::Disable**](https://msdn.microsoft.com/library/windows/hardware/hh451295)方法，调用的驱动程序[ *OnInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/hh463899)并[ *OnInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/hh463895)事件回调函数。 但是，大多数驱动程序只应允许 framework 来调用*OnInterruptEnable*并*OnInterruptDisable*在适当时间的回调函数。

 

 





