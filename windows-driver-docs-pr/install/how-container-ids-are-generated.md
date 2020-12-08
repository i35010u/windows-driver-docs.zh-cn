---
title: 如何生成容器 ID
description: 如何生成容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22de63b1c1f7beda2f0cac0ae0b84d004a027188
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839523"
---
# <a name="how-container-ids-are-generated"></a>如何生成容器 ID


从 Windows 7 开始，即插即用 (PnP) manager PnP 管理器通过以下三种机制之一为设备节点生成容器 ID (*devnode*) ：

-   总线驱动程序提供容器 ID。

    将容器 ID 分配给 devnode 时，PnP 管理器首先检查 devnode 的总线驱动程序是否可以提供容器 ID。 总线驱动程序通过 [**IRP_MN_QUERY_ID**](../kernel/irp-mn-query-id.md) 请求提供容器 ID， **IdType** 字段设置为 **BusQueryContainerID**。

    总线驱动程序可以获取嵌入到物理设备硬件中的正版容器 ID，或使用设备硬件中特定于总线的唯一 ID 生成容器 ID。 特定于总线的唯一 Id 的一些示例包括设备的序列号或设备固件中 (MAC) 地址的媒体访问控制。

    **注意**  独立硬件供应商 (IHV) 负责总线驱动程序报告的容器 ID 的唯一性。




有关详细信息，请参阅 [从 Bus-Specific 唯一 ID 生成的容器 id](container-ids-generated-from-a-bus-specific-unique-id.md)。


-   PnP 管理器通过可移动设备功能生成容器 ID。

    如果总线驱动程序无法为其枚举的 devnode 提供容器 ID，则 PnP 管理器使用可移动设备功能为设备枚举的所有 devnodes 生成容器 ID。 总线驱动程序报告此设备的功能，以响应 [**IRP_MN_QUERY_CAPABILITIES**](../kernel/irp-mn-query-capabilities.md) 的请求。

    有关详细信息，请参阅 [从可移动设备功能生成的容器 id](container-ids-generated-from-the-removable-device-capability.md)。

-   PnP 管理器通过替代可移动设备功能生成容器 ID。

    **注意**  在 Windows 10 中，DPWS 设备将始终使用此方法生成设备的容器 ID。




尽管替代机制不会更改可移动设备功能的值，但它会强制 PnP 管理器使用替代设置，而不是在为设备生成容器 Id 时使用可移动设备功能的值。

例如，如果 "可移动设备" 功能的替代指定设备可移动，则 PnP 管理器将为该设备的所有 devnodes 实例生成一个容器 ID。 无论设备是否将自身报告为可移动，都将执行此操作。

IHV 可以使用替代设备报告的可移动设备功能的密钥来填充注册表。 这种替代机制适用于不支持可移动设备功能或错误报告的传统设备。

有关详细信息，请参阅 [从可移动设备功能重写生成的容器 id](container-ids-generated-from-a-removable-device-capability-override.md)。


除了这些方法，系统还使用 ACPI BIOS 对象设置来指定设备容器分组。 有关详细信息，请参阅将 [ACPI 用于设备容器分组](using-acpi-for-device-container-grouping.md)。
