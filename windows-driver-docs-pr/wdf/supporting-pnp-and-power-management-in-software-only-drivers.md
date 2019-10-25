---
title: 支持在仅限软件的驱动程序中进行 PnP 和电源管理
description: 支持在仅限软件的驱动程序中进行 PnP 和电源管理
ms.assetid: bcfca8b2-68d6-4875-8687-27351becd6f4
keywords:
- PnP WDK KMDF、仅软件驱动程序
- 即插即用 WDK KMDF、仅软件驱动程序
- 电源管理 WDK KMDF、仅软件驱动程序
- 仅软件驱动程序 WDK KMDF
- 筛选器驱动程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 699ae5c70a48db5a94fb8017501a050a88d045c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831718"
---
# <a name="supporting-pnp-and-power-management-in-software-only-drivers"></a>支持在仅限软件的驱动程序中进行 PnP 和电源管理


*仅软件驱动程序*是指不访问任何硬件的驱动程序。 某些仅软件驱动程序驻留在不访问硬件的驱动程序堆栈中。 由于这些驱动程序不访问硬件，因此通常不需要执行任何 PnP 或电源管理操作。

其他仅软件驱动程序是筛选器驱动程序：它们驻留在一叠可访问硬件的驱动程序中，但筛选器驱动程序不访问硬件。 当筛选器驱动程序接收到指定 PnP 或电源管理操作的 i/o 请求时，驱动程序通常只将请求传递到下一个驱动程序。 框架将截获这些请求并将其传递到，因此基于框架的驱动程序永远不会看到请求。

如果你正在编写仅软件驱动程序，则驱动程序将[创建设备对象](creating-a-framework-device-object.md)，但你通常不需要提供任何事件回调函数来处理 PnP 或电源管理事件。 如果驱动程序使用[框架队列对象](framework-queue-objects.md)，则需要将**队列的** [**WDF\_IO\_queue\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)结构设置为**WdfFalse**或**WdfUseDefault**。

一些仅软件驱动程序也是[功能驱动程序](supporting-pnp-and-power-management-in-function-drivers.md)。 换句话说，单个驱动程序可以充当仅支持软件的驱动程序，以支持不访问硬件的虚拟设备，并可用作支持硬件设备的功能驱动程序。

 

 





