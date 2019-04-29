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
ms.openlocfilehash: cfb5e9d1f02c7f6d68cf8cc4c52927dc82840244
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379497"
---
# <a name="enabling-and-disabling-interrupts"></a>启用和禁用中断


如果您的驱动程序处理设备中断，它必须提供[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)并[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)回调启用和禁用中断的函数。 通常情况下，这些回调函数运行设备的 DIRQL，并且必须执行会尽一切努力启用和禁用设备的中断机制。 有关[被动等级中断](supporting-passive-level-interrupts.md)，在 IRQL 运行这些回调函数时保留了被动级别中断锁定 = passive_level 调用。

如果您的驱动程序必须执行启用或禁用中断，与相关的其他操作和这些额外的操作无法执行在 IRQL = DIRQL，驱动程序还可以提供[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540853)并[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)回调函数。 这两个回调函数运行在 IRQL = 被动\_级别有一种无中断锁保留，并且可以调用框架在 IRQL 不可用的对象方法 = DIRQL。

框架将调用的驱动程序[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)并[ *EvtDeviceD0EntryPostInterruptsEnabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540853)回调函数每次在设备进入其工作 (D0) 状态，框架已调用驱动程序的后[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)回调函数。

框架将调用的驱动程序[ *EvtDeviceD0ExitPreInterruptsDisabled* ](https://msdn.microsoft.com/library/windows/hardware/ff540856)并[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)回调函数框架将调用的驱动程序之前，设备离开其工作状态，每次[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)回调函数。 当框架将调用驱动程序的回调函数的详细信息，请参阅[PnP 和电源管理方案](pnp-and-power-management-scenarios.md)。

您必须假定框架将调用您的驱动程序的每次设备将使用相同的中断资源[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)回调函数。 有时 PnP 管理器[将重新分发的系统资源](the-pnp-manager-redistributes-system-resources.md)，并且它可能会将新 interrupt 资源分配给你的设备。

该驱动程序可以调用[ **WdfInterruptGetInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff547367)来确定设备的中断资源。 该驱动程序可以调用[ **WdfInterruptGetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff547358)来确定中断对象所属的设备。 (一些驱动程序可能会调用[ **WdfInterruptWdmGetInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff547393)。)

若要启用和禁用中断直接，驱动程序可以调用中断对象[ **WdfInterruptEnable** ](https://msdn.microsoft.com/library/windows/hardware/ff547354)并[ **WdfInterruptDisable** ](https://msdn.microsoft.com/library/windows/hardware/ff547351)方法，调用的驱动程序[ *EvtInterruptEnable* ](https://msdn.microsoft.com/library/windows/hardware/ff541730)并[ *EvtInterruptDisable* ](https://msdn.microsoft.com/library/windows/hardware/ff541714)事件回调函数。 但是，大多数驱动程序只应允许 framework 来调用*EvtInterruptEnable*并*EvtInterruptDisable*在适当时间的回调函数。

 

 





