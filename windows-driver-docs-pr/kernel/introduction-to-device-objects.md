---
title: 设备对象简介
description: 设备对象简介
ms.assetid: 310a2344-f3bc-4a7a-8e1e-63232ecd4cbe
keywords:
- 设备对象 WDK 内核，关于设备对象
- 多个设备对象 WDK 内核
- 设备堆栈 WDK 内核，关于设备堆栈
- 设备扩展 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6baed52c3e4b61f0324d84ac4ca2d1867605900e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189357"
---
# <a name="introduction-to-device-objects"></a>设备对象简介





操作系统按 *设备对象*表示设备。 一个或多个设备对象与每个设备相关联。 设备对象充当设备上所有操作的目标。

内核模式驱动程序必须为每个设备创建至少一个设备对象，但以下情况例外：

-   具有关联类或端口驱动程序的微型驱动程序不必创建自己的设备对象。 类或端口驱动程序创建设备对象，并将操作调度到微型驱动程序。

-   属于特定于设备类型的子系统的驱动程序（如 NDIS 微型端口驱动程序），其设备对象由子系统创建。

请参阅特定设备类型的文档，以确定驱动程序是否创建其自己的设备对象。

某些设备对象不表示物理设备。 仅限软件的驱动程序处理 i/o 请求，但不将这些请求传递到硬件，仍必须创建设备对象以表示其操作的目标。

有关驱动程序如何创建设备对象的详细信息，请参阅 [创建设备对象](creating-a-device-object.md)。

设备通常由多个设备对象表示，驱动程序堆栈中的每个驱动程序都有一个用于处理设备的 i/o 请求。 设备的设备对象被组织到 *设备堆栈*中。 每当在设备上执行操作时，系统都会将 [**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp) 数据结构传递到设备堆栈中顶级设备对象的驱动程序。 每个驱动程序都处理 IRP，或将其传递给与设备堆栈中的下一个较低设备对象相关联的驱动程序。 有关设备堆栈的详细信息，请参阅 [WDM 设备对象和设备堆栈](wdm-device-objects-and-device-stacks.md)。 有关 Irp 的详细信息，请参阅 [处理 irp](handling-irps.md)。

设备对象由对象管理器管理的 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 结构表示。 对象管理器为其他系统对象提供相同的设备对象功能。 具体而言，设备对象可以命名为，命名设备对象可以在其上打开句柄。 有关命名设备对象的详细信息，请参阅 [命名设备对象](named-device-objects.md)。

系统为每个设备对象（称为设备扩展）提供专用存储，驱动程序可将其用于特定于设备的存储。 系统会创建设备扩展，并将其与设备对象一起释放。 有关详细信息，请参阅 [设备扩展](device-extensions.md)。

下图说明了设备对象与 i/o 管理器之间的关系。

![阐释设备对象的关系图](images/3devobj.png)

此图显示了驱动程序编写者感兴趣的 **设备 \_ 对象** 结构的成员。 有关这些成员的详细信息，请参阅 [创建设备对象](creating-a-device-object.md)、 [初始化设备对象](initializing-a-device-object.md)和 [设备对象的属性](properties-of-device-objects.md)。

 

