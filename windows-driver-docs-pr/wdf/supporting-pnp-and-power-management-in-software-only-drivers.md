---
title: 支持在仅限软件的驱动程序中进行 PnP 和电源管理
description: 支持在仅限软件的驱动程序中进行 PnP 和电源管理
keywords:
- PnP WDK KMDF、仅软件驱动程序
- 即插即用 WDK KMDF、仅软件驱动程序
- 电源管理 WDK KMDF、仅软件驱动程序
- 仅软件驱动程序 WDK KMDF
- 筛选器驱动程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f374c86c4c68eb3a6a2c337af978bbea8df0e10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834841"
---
# <a name="supporting-pnp-and-power-management-in-software-only-drivers"></a>支持在仅限软件的驱动程序中进行 PnP 和电源管理


*仅软件驱动程序* 是指不访问任何硬件的驱动程序。 某些仅软件驱动程序驻留在不访问硬件的驱动程序堆栈中。 由于这些驱动程序不访问硬件，因此通常不需要执行任何 PnP 或电源管理操作。

其他仅软件驱动程序是筛选器驱动程序：它们驻留在一叠可访问硬件的驱动程序中，但筛选器驱动程序不访问硬件。 当筛选器驱动程序接收到指定 PnP 或电源管理操作的 i/o 请求时，驱动程序通常只将请求传递到下一个驱动程序。 框架将截获这些请求并将其传递到，因此基于框架的驱动程序永远不会看到请求。

如果你正在编写仅软件驱动程序，则驱动程序将 [创建设备对象](creating-a-framework-device-object.md) ，但你通常不需要提供任何事件回调函数来处理 PnP 或电源管理事件。 如果驱动程序使用 [框架队列对象](framework-queue-objects.md)，则需要将队列的 [**WDF \_ IO \_ 队列 \_ CONFIG**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)结构的 **PowerManaged** 成员设置为 **WdfFalse** 或 **WdfUseDefault**。

一些仅软件驱动程序也是 [功能驱动程序](supporting-pnp-and-power-management-in-function-drivers.md)。 换句话说，单个驱动程序可以充当仅支持软件的驱动程序，以支持不访问硬件的虚拟设备，并可用作支持硬件设备的功能驱动程序。

 

