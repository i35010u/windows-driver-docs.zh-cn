---
title: 编写 DriverEntry 例程
description: 编写 DriverEntry 例程
keywords:
- 标准驱动程序例程 WDK 内核，DriverEntry 例程
- 驱动程序例程 WDK 内核，DriverEntry 例程
- 例程 WDK 内核，DriverEntry 例程
- DriverEntry WDK 内核
- DriverEntry WDK 内核，关于 DriverEntry 例程
- 驱动程序初始化 WDK 内核
- 初始化驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a03400e0d06f01eb4a54780813c42bfb3921771
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782633"
---
# <a name="writing-a-driverentry-routine"></a>编写 DriverEntry 例程





每个驱动程序都必须有一个 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程，该例程初始化驱动程序范围内的数据结构和资源。 当 i/o 管理器加载驱动程序时，它会调用 **DriverEntry** 例程。

在支持即插即用 (PnP) 的驱动程序中，由于所有驱动程序都应该， **DriverEntry** 例程负责 *驱动程序* 初始化，而 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程 (和（可能为）处理 PnP [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求) 的调度例程负责 *设备* 初始化。 驱动程序初始化包括导出驱动程序的其他入口点、初始化驱动程序使用的某些对象，以及设置各种每驱动程序系统资源。  (非 PnP 驱动程序的要求明显不同，如 \[ \] MICROSOFT Windows NT 4.0 及更早版本的驱动程序开发工具包 DDK 中所述。 ) 

**DriverEntry** 例程在系统线程的上下文中以 IRQL = 被动级别进行调用 \_ 。

**DriverEntry** 例程可以是可分页的，并且应在 INIT 段中，因此将被丢弃。 使用 " **分配 \_ 文本** 杂注指令"，如随 Windows 驱动程序工具包一起提供的示例驱动程序 (WDK) 中所示。

本节包含下列主题：

[DriverEntry 的必要责任](driverentry-s-required-responsibilities.md)

[DriverEntry 的可选责任](driverentry-s-optional-responsibilities.md)

[DriverEntry 返回值](driverentry-return-values.md)

 

