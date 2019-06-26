---
title: 有关设备对象的要点
description: 有关设备对象的要点
ms.assetid: 4c54340b-3b4c-4c67-b28d-fac769e4feb7
keywords:
- 设备对象 WDK 内核，设计注意事项
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4dc0760f01dbc565109c96cf0c2070d377a5a1b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369709"
---
# <a name="points-to-consider-about-device-objects"></a>有关设备对象的要点





设计的内核模式驱动程序时，请记住以下几点：

-   除了某些文件系统驱动程序，所有 I/O 操作始终都发送到设备堆栈的顶部的设备对象。

-   使用指定的设备对象的名称，在堆栈中或使用该名称，如符号链接或设备接口的别名来标识设备堆栈。 有关 WDM 函数驱动程序，通过设备的总线驱动程序创建指定的设备对象。 非 WDM 驱动程序必须创建其自己命名的设备对象。

-   最低级别驱动程序，如即插即用硬件总线驱动程序，为其控制每个设备创建一个物理设备对象 (PDO)。 中间驱动程序，即插即用功能驱动程序，如创建功能的设备对象 (FDO)。

    WDM 驱动程序创建中的设备对象及其[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)后设备枚举即插即用管理器将调用的例程。

-   对于大多数最低级别和中间驱动程序，每个设备对象的设备扩展是每个驱动程序的主 （并且通常只有一个） 的全局数据存储区中。 许多驱动程序维护设备状态和所有其他特定于设备的数据和驱动程序需要在每个驱动程序创建的设备对象的驱动程序定义的设备扩展中的资源。

    (此外，驱动程序特定[I/O 堆栈位置](i-o-stack-locations.md)与关联 IRP 可被视为对于某些类型的数据的特定于操作的本地存储区。)

特定驱动程序必须创建设备对象的详细信息，请参阅 Windows Driver Kit (WDK) 中的特定于设备的类型的文档。

 

 




