---
title: 标准驱动程序的常规要求
description: 标准驱动程序的常规要求
ms.assetid: 49b382ad-c282-41d2-b8b3-68eca4e12b9c
keywords:
- 标准驱动程序例程 WDK 内核要求
- 驱动程序例程 WDK 内核要求
- 例程 WDK 内核要求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf8a7ddcc099410a4741f8ecb00040ef9721f68b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541068"
---
# <a name="standard-driver-routine-requirements"></a>标准驱动程序的常规要求





设计的内核模式驱动程序时，请记住以下几点：

-   每个驱动程序必须具有[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，初始化驱动程序范围内的数据结构和资源。 I/O 管理器调用**DriverEntry**例程时加载驱动程序。

-   每个驱动程序必须具有至少一个调度例程用于接收和处理 I/O 请求数据包 (Irp)。 每个驱动程序必须将放置中的调度例程的入口点及其[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)结构，每个[IRP 主要函数代码](https://msdn.microsoft.com/library/windows/hardware/ff550710)的驱动程序可以接收。 驱动程序可以具有每个 IRP 主要函数代码中，一个单独的调度例程也可以有一个或多个处理多个函数代码的调度例程。

-   每个 WDM 驱动程序必须具有[ *Unload* ](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程。 该驱动程序必须将放*Unload*驱动程序的驱动程序对象中的例程的入口点。 职责[PnP 驱动程序的卸载例程](pnp-driver-s-unload-routine.md)非常小，但[非 PnP 驱动程序的卸载例程](non-pnp-driver-s-unload-routine.md)会释放该驱动程序使用任何系统资源。

-   每个 WDM 驱动程序必须具有*AddDevice*的驱动程序对象。 *AddDevice*例程负责创建和初始化设备用于每个即插即用设备驱动程序控件对象。

-   驱动程序可以具有[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程，该驱动程序的启动 I/O 操作的 Irp 调用 I/O 管理器已排队到系统提供 IRP 队列。 不具有任何驱动程序*StartIo*或例程必须设置并管理内部队列的 Irp 接收，则必须完成其调度例程中的每个 IRP。 更高级别的驱动程序可能不具有*StartIo*例程中，如果它们只需将 Irp 传递到较低级别的驱动程序直接从其调度例程。

-   某些微型端口驱动程序是上述要求的例外情况。 请参阅特定于设备的类型的文档了解微型端口驱动程序要求在 Windows Driver Kit (WDK)。

-   驱动程序是否包含任何其他类型的标准例程取决于其功能以及如何将该驱动程序适用于系统 （例如，无论它与互操作系统提供的驱动程序）。 请参阅 WDK 的详细信息中的设备类型特定文档。

 

 




