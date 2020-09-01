---
title: 释放设备和控制器对象
description: 释放设备和控制器对象
ms.assetid: 35404401-d3a8-4257-b1a3-b16ebe42b181
keywords:
- 卸载例程 WDK 内核，非 PnP 驱动程序
- 非 PnP 卸载例程 WDK 内核
- 正在释放设备
- 释放控制器对象
- 设备释放 WDK 内核
- 控制器对象 WDK 内核，释放
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a1dee7d52069731ffd411cc7fdd7f917263fd8a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191453"
---
# <a name="releasing-device-and-controller-objects"></a>释放设备和控制器对象





驱动程序在删除设备或控制器对象之前，必须释放对外部资源（如指向其他驱动程序的对象的指针和/或中断对象）的引用，并将其存储在相应的设备或控制器扩展中。 然后，它可以为驱动程序创建的每个设备对象调用 [**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice) 。 之前调用 [**IoCreateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller) 的非 WDM 驱动程序也必须调用 [**IoDeleteController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)。

当 [*Unload*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程使用相应的设备对象调用 **IoDeleteDevice** 时，驱动程序在设备扩展中提供存储的任何内核定义的对象都将自动释放。 通常，如果驱动程序为其设备扩展[*Reinitialize*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)中的对象提供存储，则通过调用**KeInitialize * Xxx***[**设置的任何**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)对象都可以通过调用**IoDeleteDevice**释放。 例如，如果驱动程序具有 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983) 例程，并且为其设备扩展中的必需 DPC 和定时器对象提供了存储，则调用 **IoDeleteDevice** 会释放这些系统资源。

同样，当 *Unload* 例程使用相应的控制器对象调用 **IoDeleteController** 时，驱动程序在控制器扩展中提供存储的任何内核定义的对象都将自动释放。

如果名为[**IoGetConfigurationInformation**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetconfigurationinformation)的**DriverEntry**或重新*初始化*例程递增特定类型的设备的计数，则在 i/o 管理器的全局配置信息结构中删除相应的设备对象时，该*卸载*例程还必须调用**IoGetConfigurationInformation**并减小其设备的计数。

在返回 control 之前， *Unload* 例程还负责释放其他驱动程序例程尚未释放的任何其他由驱动程序分配的资源。

 

