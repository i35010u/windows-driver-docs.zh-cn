---
title: 存储类驱动程序的 RemoveDevice 例程
description: 存储类驱动程序的 RemoveDevice 例程
ms.assetid: fbcbfbab-676a-43d3-aa63-0ea5e5f265d2
keywords:
- RemoveDevice
- 查询-删除请求 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bbe81c56d26e1de1e97380c8f353d552e424acc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845288"
---
# <a name="storage-class-drivers-removedevice-routine"></a>存储类驱动程序的 RemoveDevice 例程


## <span id="ddk_storage_class_drivers_removedevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_REMOVEDEVICE_ROUTINE_KG"></span>


当要删除设备时，PnP 管理器首先使用 PnP 查询-删除请求（IRP [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)\_MJ\_pnp，并使用[**irp\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)。 在以下任何情况下，存储类驱动程序都应将查询删除请求失败：

-   设备包含系统分页文件或休眠文件。

-   驱动程序正在运行一个不应取消的长时间操作（例如，倒带或格式化磁带）。

-   设备有未完成的句柄（创建）。

如果设备被声称崩溃转储，则存储类驱动程序也可能会导致查询删除请求失败，因为删除此类设备会禁用故障转储。

如果存储类驱动程序返回状态\_"成功" 以响应查询-删除请求，则 PnP 管理器将使用 PnP 删除请求（IRP\_MJ\_PNP 和 IRP\_MN 调用类驱动程序的*DispatchPnP*例程[ **\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)）。 存储类驱动程序的*DispatchPnP*例程要么调用内部*RemoveDevice*例程，要么实现同一功能内联。

存储类驱动程序的*RemoveDevice*例程必须执行以下操作：

-   释放驱动程序分配的所有未完成的资源，例如内存或事件。

-   删除驱动程序创建的符号链接（如果有）。

-   删除设备对象（FDO）。

-   将请求转发到下一个较低版本的驱动程序。

如果存储类驱动程序在启动时创建 PDOs （例如，表示分区媒体设备上的分区），则当 PnP 管理器将删除请求发送到存储类驱动程序时，此类 PDOs 已被删除。

即使在设备对象被删除后，如果它有非零引用计数，设备对象在系统中仍保持不变，直到其引用计数变为零时，才会以静默方式消失。 存储类驱动程序在删除设备对象之后不得尝试使用设备对象指针。

有关处理删除请求的详细信息，请参阅[删除设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)。

 

 




