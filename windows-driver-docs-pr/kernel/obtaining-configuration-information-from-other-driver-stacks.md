---
title: 从其他驱动程序堆栈获取配置信息
description: 从其他驱动程序堆栈获取配置信息
keywords:
- I/o WDK 内核，设备配置空间
- 设备配置空间 WDK i/o
- 配置空间 WDK i/o
- 太空 WDK i/o
- 驱动程序堆栈 WDK 配置信息
- BUS_INTERFACE_STANDARD
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfbd4fb0998779e41d35f54fc4c641b2ba076fa1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803545"
---
# <a name="obtaining-configuration-information-from-other-driver-stacks"></a>从其他驱动程序堆栈获取配置信息





有时，您需要从设备的驱动程序所在的设备的配置空间中获取信息，而该设备的驱动程序与驱动程序所在的堆栈不同。 例如，假设要在 PCI 到 PCI 桥的配置空间中设置一个位，并且没有指向桥的 PDO 的指针。 尽管操作系统会枚举 PCI 到 PCI 桥，并为系统上的每个桥创建一个 PDO，但不会为这些设备注册设备接口。 因此，不能使用设备接口机制访问这些桥的配置空间。 有关设备接口的详细信息，请参阅 [设备接口简介](../install/overview-of-device-interface-classes.md)。

在 Windows NT 4.0 中，驱动程序可以使用 [**HalGetBusData**](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) 和 [**HalSetBusData**](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) 例程访问此类设备的配置空间。 在 Windows 2000 和更高版本的 Windows 中，这种情况并不是这样。

Windows 2000 和更高版本的 Windows 不允许驱动程序访问属于其他驱动程序堆栈的硬件。 可以编写筛选器驱动程序来提供所需的功能。 例如，如果想要访问桥硬件，则必须设计一个筛选器驱动程序，该驱动程序在桥的配置空间上实现所需的操作。 还必须提供一个 INF 文件，用于指定桥硬件的可能的硬件 Id，以便在检测到桥的设备 ID 时，PnP 管理器可以将筛选器驱动程序加载到桥的驱动程序堆栈上。

或者，你可以使用设备的共同安装程序中的 **SetupDi <em>Xxx</em>** 函数以编程方式安装筛选器。

然后，筛选器驱动程序可以使用 [**总线 \_ 接口 \_ 标准**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard) 接口访问桥。

 

