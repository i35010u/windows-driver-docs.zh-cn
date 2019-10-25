---
title: 有关设备对象的要点
description: 有关设备对象的要点
ms.assetid: 4c54340b-3b4c-4c67-b28d-fac769e4feb7
keywords:
- 设备对象 WDK 内核，设计注意事项
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb92f7acf5f5f8d6488c1afcf7774dd657c293c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827671"
---
# <a name="points-to-consider-about-device-objects"></a>有关设备对象的要点





设计内核模式驱动程序时，请记住以下几点：

-   除了某些文件系统驱动程序，所有 i/o 操作始终发送到设备堆栈的顶级设备对象。

-   使用堆栈中命名设备对象的名称或使用该名称的别名（如符号链接或设备接口）来标识设备堆栈。 对于 WDM 函数驱动程序，指定的设备对象由设备的总线驱动程序创建。 非 WDM 驱动程序必须创建其自己的命名设备对象。

-   最低级别的驱动程序（例如 PnP 硬件总线驱动程序）会为其控制的每个设备创建一个物理设备对象（PDO）。 中间驱动程序（例如 PnP 函数驱动程序）将创建一个功能设备对象（FDO）。

    WDM 驱动程序在其[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中创建设备对象，在设备枚举后由 PnP 管理器调用。

-   对于最底层和中间的驱动程序，每个设备对象的设备扩展是每个驱动程序的主要（并且通常只是）全局数据存储区。 许多驱动程序会在驱动程序所创建的每个设备对象的驱动程序定义的设备扩展中维护设备状态以及驱动程序所需的所有其他特定于设备的数据和资源。

    （此外，可以将与 IRP 关联的特定于驱动程序的[i/o 堆栈位置](i-o-stack-locations.md)视为某些类型的数据的特定于操作的本地存储区域。）

有关特定驱动程序必须创建的设备对象的详细信息，请参阅 Windows 驱动程序工具包（WDK）中的特定于设备类型的文档。

 

 




