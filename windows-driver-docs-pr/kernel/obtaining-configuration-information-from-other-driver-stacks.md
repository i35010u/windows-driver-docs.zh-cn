---
title: 从其他驱动程序堆栈获取配置信息
description: 从其他驱动程序堆栈获取配置信息
ms.assetid: ca0f3d51-24c6-44df-828f-6aeb2565c1ae
keywords:
- I/O WDK 内核，设备配置空间
- 设备配置空间 WDK I/O
- 配置空间 WDK I/O
- 空间 WDK I/O
- 驱动程序堆栈 WDK 配置信息
- BUS_INTERFACE_STANDARD
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: be7a62b87faeeb5d15eb9614b66a8e44db9a8615
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384934"
---
# <a name="obtaining-configuration-information-from-other-driver-stacks"></a>从其他驱动程序堆栈获取配置信息





有时您需要从其驱动程序而不是您的驱动程序位于堆栈上的设备的配置空间获取信息。 例如，假设你想要设置一个位 PCI PCI 桥的配置空间中并且没有指向的是 PDO 的桥的指针。 虽然操作系统枚举 PCI PCI 桥，并在系统上创建的每个桥 PDO，但是它不会注册这些设备的设备接口。 因此，不能使用设备接口机制来访问这些桥的配置空间。 有关设备接口的详细信息请参阅[简介设备接口](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)。

在 Windows NT 4.0 中的驱动程序无法访问使用此类设备的配置空间[ **HalGetBusData** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))并[ **HalSetBusData** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))例程。 在 Windows 2000 和更高版本的 Windows 中，这不再是这种情况。

Windows 2000 和更高版本的 Windows 不允许访问属于其他驱动程序堆栈的硬件的驱动程序。 可以编写筛选器驱动程序来提供所需的功能。 如果你想要访问桥硬件，例如，必须设计实现在桥的配置空间所需的操作筛选器驱动程序。 此外必须提供指定桥硬件可能存在的硬件 Id，因此检测到桥的设备 ID 时，即插即用管理器可以加载到桥的驱动程序堆栈上的筛选器驱动程序的 INF 文件。

或者，可以安装以编程方式使用的筛选器**SetupDi * Xxx*** 你的设备的共同安装程序中的函数。

然后，筛选器驱动程序可以访问桥使用[**总线\_界面\_标准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_bus_interface_standard)接口。

 

 




