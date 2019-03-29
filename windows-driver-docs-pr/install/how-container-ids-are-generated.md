---
title: 如何生成容器 ID
description: 如何生成容器 ID
ms.assetid: baa3c045-05ee-4012-97a3-c6e575c897be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59224a00be8a9686389c0b859e6b2da65ae1a811
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567166"
---
# <a name="how-container-ids-are-generated"></a>如何生成容器 ID


从 Windows 7 开始，插即用 (PnP) 管理器生成的设备节点的容器 ID (*devnode*) 通过三种机制之一：

-   总线驱动程序提供容器 id。

    将容器 ID 分配给 devnode，即插即用管理器首先检查是否 devnode 的总线驱动程序可以提供一个容器 id。 总线驱动程序提供容器 ID 通过[ **IRP_MN_QUERY_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff551679)请求**Parameters.QueryId.IdType**字段设置为**BusQueryContainerID**.

    总线驱动程序可以获取物理设备硬件中嵌入的正版容器 ID 或使用来自设备硬件的特定于总线的唯一 ID 生成的容器 id。 特定于总线的唯一 Id 的一些示例包括设备的序列号或设备的固件中的媒体访问控制 (MAC) 地址。

    **请注意**独立硬件供应商 (IHV) 负责容器 ID 由总线驱动程序报告的唯一性。




有关详细信息，请参阅[从特定于总线的唯一 ID 生成的容器 Id](container-ids-generated-from-a-bus-specific-unique-id.md)。


-   PnP 管理器生成通过可移动设备功能的容器 ID。

    如果总线驱动程序不能为它枚举 devnode 提供容器的 ID，即插即用 manager 将使用可移动设备功能来生成所有 devnodes 枚举设备的容器 ID。 总线驱动程序报告此设备功能，以响应[ **IRP_MN_QUERY_CAPABILITIES** ](https://msdn.microsoft.com/library/windows/hardware/ff551664)请求。

    有关详细信息，请参阅[从可移动设备功能生成的容器 Id](container-ids-generated-from-the-removable-device-capability.md)。

-   PnP 管理器生成的可移动设备功能重写通过容器 ID。

    **请注意**在 Windows 10 中，DPWS 设备将始终生成使用此方法在设备的容器 ID。




尽管替代机制不会更改可移动设备功能的值，它会强制 PnP 管理器中，替代设置而不是可移动设备功能的值生成时要使用设备的容器 Id。

例如，如果可移动设备功能的重写指定设备为可移动，即插即用 manager 会生成所有 devnodes 枚举设备的容器 ID。 无论是否在设备自身报告为可移动或不执行此操作。

IHV 可以使用密钥重写由设备报告了可移动设备功能填充注册表。 此替代机制可用于不支持可移动设备功能或者错误地报告的旧设备。

有关详细信息，请参阅[从可移动设备功能替代生成的容器 Id](container-ids-generated-from-a-removable-device-capability-override.md)。


除了这些方法，系统使用 ACPI BIOS 对象设置指定设备容器分组。 有关详细信息，请参阅[使用的设备容器分组的 ACPI](using-acpi-for-device-container-grouping.md)。









