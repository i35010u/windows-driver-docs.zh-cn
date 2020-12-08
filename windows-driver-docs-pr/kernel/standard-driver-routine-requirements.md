---
title: 标准驱动程序例程要求
description: 标准驱动程序例程要求
keywords:
- 标准驱动程序例程 WDK 内核，要求
- 驱动程序例程 WDK 内核，要求
- 例程的 WDK 内核，要求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff7fa2dba26ffb672de6529250837ccabdc530d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837947"
---
# <a name="standard-driver-routine-requirements"></a>标准驱动程序例程要求





设计内核模式驱动程序时，请记住以下几点：

-   每个驱动程序都必须有一个 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程，该例程初始化驱动程序范围内的数据结构和资源。 当 i/o 管理器加载驱动程序时，它会调用 **DriverEntry** 例程。

-   每个驱动程序必须具有至少一个用于接收和处理 i/o 请求数据包 (Irp) 的调度例程。 每个驱动程序都必须在其 [**驱动程序 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object) 结构中放置一个调度例程的入口点，以便驱动程序可以接收的每个 [IRP 主要功能代码](./irp-major-function-codes.md) 。 对于每个 IRP 主要功能代码，驱动程序可以有一个单独的调度例程，也可以有一个或多个调度例程来处理多个函数代码。

-   每个 WDM 驱动程序都必须有一个 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程。 驱动程序必须将 *卸载* 例程的入口点置于驱动程序的驱动程序对象中。 [PnP 驱动程序的卸载例程](pnp-driver-s-unload-routine.md)的责任非常小，但[非 PnP 驱动程序的 unload 例程](non-pnp-driver-s-unload-routine.md)负责释放驱动程序所使用的任何系统资源。

-   每个 WDM 驱动程序都必须有一个 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程，并定义驱动程序对象的 *驱动程序扩展* 中的入口点。 *AddDevice* 例程负责为驱动程序控制的每个 PnP 设备创建和初始化设备对象。

-   驱动程序可以有一个 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程，i/o 管理器会调用它来启动对 irp 的 i/o 操作。该驱动程序已排入系统提供的 irp 队列。 任何没有 *StartIo* 例程的驱动程序都必须设置和管理其接收的 irp 的内部队列，或者必须在其调度例程内完成每个 irp。 如果较高级别的驱动程序只是直接从调度例程将 Irp 传递到较低级别的驱动程序，则可能没有 *StartIo* 的例程。

-   某些微型端口驱动程序是前述要求的例外情况。 有关微型端口驱动程序要求的信息，请参阅 Windows 驱动程序工具包中的设备特定于设备的文档 (WDK) 。

-   驱动程序是否有任何其他类型的标准例程取决于其功能以及该驱动程序如何适合系统 (例如，它是否与系统提供的驱动程序) 互操作。 有关详细信息，请参阅 WDK 中设备类型的特定文档。

