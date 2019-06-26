---
title: 编写 DriverEntry 例程
description: 编写 DriverEntry 例程
ms.assetid: c33bc82b-6181-4e31-b272-aaadb2d9b058
keywords:
- 标准驱动程序例程 WDK 内核，DriverEntry 例程
- 驱动程序例程 WDK 内核，DriverEntry 例程
- 例程 WDK 内核，DriverEntry 例程
- DriverEntry WDK 内核
- DriverEntry WDK 内核，有关 DriverEntry 例程
- 驱动程序初始化 WDK 内核
- 初始化驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc16d18213a3f73e2c265040bdca372cca294e35
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374149"
---
# <a name="writing-a-driverentry-routine"></a>编写 DriverEntry 例程





每个驱动程序必须具有[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程，初始化驱动程序范围内的数据结构和资源。 I/O 管理器调用**DriverEntry**例程时加载驱动程序。

支持的所有驱动程序应，插即用 (PnP) 驱动程序中**DriverEntry**例程负责*驱动程序*初始化，而[ *AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程 (和可能是，处理即插即用的调度例程[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求) 是负责*设备*初始化。 驱动程序初始化包括导出驱动程序的初始化其他入口点特定对象的驱动程序使用和设置每个驱动程序的各种系统资源。 (非 PnP 驱动程序具有明显不同的要求，如驱动程序开发工具包中所述\[DDK\] Microsoft Windows NT 4.0 及更早版本。)

**DriverEntry**例程会在 IRQL 在系统线程的上下文中调用 = 被动\_级别。

一个**DriverEntry**例程可以为可分页，应为 INIT 段中，因此它将被放弃。 使用**alloc\_文本**杂注指令，如示例驱动程序提供了使用 Windows Driver Kit (WDK) 中所示。

本部分包含以下主题：

[DriverEntry 的必须承担的责任](driverentry-s-required-responsibilities.md)

[DriverEntry 的可选职责](driverentry-s-optional-responsibilities.md)

[DriverEntry 返回值](driverentry-return-values.md)

 

 




