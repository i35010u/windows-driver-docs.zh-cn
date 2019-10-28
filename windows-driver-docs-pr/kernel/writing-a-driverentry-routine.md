---
title: 编写 DriverEntry 例程
description: 编写 DriverEntry 例程
ms.assetid: c33bc82b-6181-4e31-b272-aaadb2d9b058
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
ms.openlocfilehash: 965ba1329242a88fa6ce67a027d936bc6019c916
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835624"
---
# <a name="writing-a-driverentry-routine"></a>编写 DriverEntry 例程





每个驱动程序都必须有一个[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程，该例程初始化驱动程序范围内的数据结构和资源。 当 i/o 管理器加载驱动程序时，它会调用**DriverEntry**例程。

在支持即插即用（PnP）的驱动程序中，如果所有驱动程序都应该， **DriverEntry**例程负责*驱动程序*初始化，而[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程（并且可能是处理 PnP IRP 的调度例程[ **\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求）负责*设备*初始化。 驱动程序初始化包括导出驱动程序的其他入口点、初始化驱动程序使用的某些对象，以及设置各种每驱动程序系统资源。 （非 PnP 驱动程序的要求明显不同，如驱动程序开发工具包 \[DDK\] Microsoft Windows NT 4.0 及更早版本中所述。）

**DriverEntry**例程在系统线程的上下文中调用，以 IRQL = 被动\_级别。

**DriverEntry**例程可以是可分页的，并且应在 INIT 段中，因此将被丢弃。 如随 Windows 驱动程序工具包（WDK）提供的示例驱动程序所示，请使用**分配\_文本**杂注指令。

本部分包含以下主题：

[DriverEntry 所需的职责](driverentry-s-required-responsibilities.md)

[DriverEntry 的可选责任](driverentry-s-optional-responsibilities.md)

[DriverEntry 返回值](driverentry-return-values.md)

 

 




