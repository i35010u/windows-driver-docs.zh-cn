---
title: 从特定于总线的唯一 ID 生成的容器 ID
description: 从特定于总线的唯一 ID 生成的容器 ID
ms.assetid: 06bd4f06-51f2-4983-9ddc-bff27eaa367e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a82c584ae4cf3c09b427f1b80bde8c677b26af4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356333"
---
# <a name="container-ids-generated-from-a-bus-specific-unique-id"></a>从特定于总线的唯一 ID 生成的容器 ID


生成的容器 ID 的设备的首选的方法基于特定于总线的唯一 id。 这是生成的容器 Id 的最精确和最可靠方法。

插即用 (PnP) 管理器使用此方法，如果满足以下条件：

-   设备包含特定于总线的唯一 id。

-   设备的总线驱动程序会将此唯一 ID 识别为存在且格式正确。

-   总线驱动程序可以可靠地哈希处理的唯一 ID 为全局唯一标识符 (*GUID*)，并在响应中返回此 GUID [ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)函数代码中**Parameters.QueryId.IdType**的成员[ **IO_STACK_LOCATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构设置为**BusQueryContainerID**.

Windows 7 和更高版本的 Windows 提供的多个最常见的总线类型收件箱驱动程序。 这包括 USB、 蓝牙和 PNP-X 的。 设备仅对于这些总线类型，需要包含特定于总线的唯一 id。 提供的 Windows 总线驱动程序然后将从设备读取的唯一 ID 并创建一个容器 id。

下面的主题介绍收件箱总线驱动程序生成特定的总线类型的容器 Id 的方式：

[USB 设备的容器 Id](container-ids-for-usb-devices.md)

[蓝牙设备的容器 Id](container-ids-for-bluetooth-devices.md)

[PNP-X 的设备的容器 Id](container-ids-for-pnp-x-devices.md)

[1394 设备的容器 Id](container-ids-for-1394-devices.md)

[ESATA 设备的容器 Id](container-ids-for-esata-devices.md)

[PCI Express 设备的容器 Id](container-ids-for-pci-express-devices.md)

 

 





