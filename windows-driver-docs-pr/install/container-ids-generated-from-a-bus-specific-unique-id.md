---
title: 从特定于总线的唯一 ID 生成的容器 ID
description: 从特定于总线的唯一 ID 生成的容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3ede6c0db590cf1f3e08cc643f21589ef92b01f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782951"
---
# <a name="container-ids-generated-from-a-bus-specific-unique-id"></a>从特定于总线的唯一 ID 生成的容器 ID


为设备生成容器 ID 的首选方式基于特定于总线的唯一 ID。 这是生成容器 Id 的最准确、最可靠的方法。

如果满足以下条件，则即插即用 (PnP) 管理器使用此方法：

-   设备包含特定于总线的唯一 ID。

-   设备的总线驱动程序将此唯一 ID 识别为存在并且格式正确。

-   总线驱动程序可以将唯一 ID 可靠地散列到全局唯一标识符 (*GUID*) ，并在 [**IO_STACK_LOCATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的 **IdType** 成员设置为 **BusQueryContainerID** 时返回此 GUID 以响应 [**IRP_MN_QUERY_ID**](../kernel/irp-mn-query-id.md)函数代码。

Windows 7 和更高版本的 Windows 为多个最常见的总线类型提供了收件箱驱动程序。 这包括 USB、蓝牙和 Pnp-x。 对于这些总线类型，只需将设备包含特定于总线的唯一 ID。 然后，提供的 Windows bus 驱动程序将从设备读取唯一 ID 并创建容器 ID。

以下主题介绍收件箱总线驱动程序如何为某些总线类型生成容器 Id：

[USB 设备的容器 ID](./how-usb-devices-are-assigned-container-ids.md)

[蓝牙设备的容器 ID](container-ids-for-bluetooth-devices.md)

[PnP-X 设备的容器 ID](container-ids-for-pnp-x-devices.md)

[1394 设备的容器 ID](container-ids-for-1394-devices.md)

[eSATA 设备的容器 ID](container-ids-for-esata-devices.md)

[PCI Express 设备的容器 ID](container-ids-for-pci-express-devices.md)

