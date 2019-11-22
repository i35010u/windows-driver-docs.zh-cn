---
title: 从特定于总线的唯一 ID 生成的容器 ID
description: 从特定于总线的唯一 ID 生成的容器 ID
ms.assetid: 06bd4f06-51f2-4983-9ddc-bff27eaa367e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60603d68d5354c42ecf79f573fb7025fed8f6013
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840651"
---
# <a name="container-ids-generated-from-a-bus-specific-unique-id"></a>从特定于总线的唯一 ID 生成的容器 ID


为设备生成容器 ID 的首选方式基于特定于总线的唯一 ID。 这是生成容器 Id 的最准确、最可靠的方法。

如果满足以下条件，则即插即用（PnP）管理器使用此方法：

-   设备包含特定于总线的唯一 ID。

-   设备的总线驱动程序将此唯一 ID 识别为存在并且格式正确。

-   总线驱动程序可以将唯一 ID 可靠地哈希到全局唯一标识符（*GUID*），并在将[**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的**QueryId. IdType**成员设置为**BusQueryContainerID**时返回此 GUID 以响应[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)的函数代码。

Windows 7 和更高版本的 Windows 为多个最常见的总线类型提供了收件箱驱动程序。 这包括 USB、蓝牙和 Pnp-x。 对于这些总线类型，只需将设备包含特定于总线的唯一 ID。 然后，提供的 Windows bus 驱动程序将从设备读取唯一 ID 并创建容器 ID。

以下主题介绍收件箱总线驱动程序如何为某些总线类型生成容器 Id：

[USB 设备的容器 Id](container-ids-for-usb-devices.md)

[蓝牙设备的容器 Id](container-ids-for-bluetooth-devices.md)

[Pnp-x 设备的容器 Id](container-ids-for-pnp-x-devices.md)

[1394设备的容器 Id](container-ids-for-1394-devices.md)

[ESATA 设备的容器 Id](container-ids-for-esata-devices.md)

[PCI Express 设备的容器 Id](container-ids-for-pci-express-devices.md)

 

 





