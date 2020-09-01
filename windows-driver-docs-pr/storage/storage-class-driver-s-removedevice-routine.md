---
title: 存储类驱动程序的 RemoveDevice 例程
description: 存储类驱动程序的 RemoveDevice 例程
ms.assetid: fbcbfbab-676a-43d3-aa63-0ea5e5f265d2
keywords:
- RemoveDevice
- 查询-删除请求 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40e6a16b6be95be3e060789457b18916c2663137
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193061"
---
# <a name="storage-class-drivers-removedevice-routine"></a>存储类驱动程序的 RemoveDevice 例程


## <span id="ddk_storage_class_drivers_removedevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_REMOVEDEVICE_ROUTINE_KG"></span>


当要删除设备时，PnP 管理器首先使用 PnP 查询删除请求来调用类驱动程序的 [**DispatchPnP**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程， (irp \_ MJ \_ PnP with [**irp \_ MN \_ 查询 " \_ 删除 \_ 设备**](../kernel/irp-mn-query-remove-device.md)"。 在以下任何情况下，存储类驱动程序都应将查询删除请求失败：

-   设备包含系统分页文件或休眠文件。

-   驱动程序正在运行长时间的操作，此操作不应被取消 (例如，倒带或格式化磁带) 。

-    (创建) 的设备有未完成的句柄。

如果设备被声称崩溃转储，则存储类驱动程序也可能会导致查询删除请求失败，因为删除此类设备会禁用故障转储。

如果存储类驱动程序返回状态 \_ "成功" 以响应查询-删除请求，则 pnp 管理器会调用类驱动程序的 *DispatchPnP* 例程，其中包含 PnP 删除请求 (irp \_ MJ \_ PnP with [**irp \_ MN \_ remove \_ DEVICE**](../kernel/irp-mn-remove-device.md)) 。 存储类驱动程序的 *DispatchPnP* 例程要么调用内部 *RemoveDevice* 例程，要么实现同一功能内联。

存储类驱动程序的 *RemoveDevice* 例程必须执行以下操作：

-   释放驱动程序分配的所有未完成的资源，例如内存或事件。

-   删除驱动程序创建的符号链接（如果有）。

-    (FDO) 中删除设备对象。

-   将请求转发到下一个较低版本的驱动程序。

如果存储类驱动程序在启动时创建了 PDOs (例如，表示分区媒体设备) 上的分区，则当 PnP 管理器将删除请求发送到存储类驱动程序时，此类 PDOs 已被删除。

即使在设备对象被删除后，如果它有非零引用计数，设备对象在系统中仍保持不变，直到其引用计数变为零时，才会以静默方式消失。 存储类驱动程序在删除设备对象之后不得尝试使用设备对象指针。

有关处理删除请求的详细信息，请参阅 [删除设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/removing-a-device)。

 

