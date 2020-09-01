---
title: 设置存储类驱动程序的设备扩展
description: 设置存储类驱动程序的设备扩展
ms.assetid: 9d050d23-39c0-406e-9f4b-2e95d388f5cf
keywords:
- 存储类驱动程序 WDK，设备扩展
- 类驱动程序 WDK 存储，设备扩展
- 设备扩展 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f339755e582e1d522dad434893177d7c4fb5d4d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191281"
---
# <a name="setting-up-a-storage-class-drivers-device-extension"></a>设置存储类驱动程序的设备扩展


## <span id="ddk_setting_up_a_storage_class_drivers_device_extension_kg"></span><span id="DDK_SETTING_UP_A_STORAGE_CLASS_DRIVERS_DEVICE_EXTENSION_KG"></span>


在存储类驱动程序所创建的每个设备对象的 [设备扩展](../kernel/device-extensions.md) 中，该驱动程序为其用来管理设备 i/o 请求的驱动程序所用的任何数据（例如指向传递到 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)的 PDO 的 [**指针、指向**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)其自己的设备对象的返回指针和指向其自己的设备对象的指针等）提供存储。

大多数存储类驱动程序还为以下信息提供存储：

-   特定于设备类型的超时值

    类驱动程序可以在它发送到端口驱动程序的 SRBs 中传递超时值，这是 SRB \_ 函数 \_ 执行 scsi 请求的时间， \_ (参见代表每个类驱动程序) [**SCSI \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block) 。 **SrbStatus** \_ \_ 如果端口驱动程序将请求发送到基础驱动程序并在请求完成后超过指定的超时值，则端口驱动程序将返回 SRB，并将其 SRBSTATUS 成员设置为 SRB 状态超时。

-   指向类驱动程序的错误处理例程的指针

    有关存储类驱动程序中的错误处理的详细信息，请参阅 [存储类驱动程序的 IoCompletion 例程](storage-class-driver-s-iocompletion-routines.md) 。

-   驱动程序在设备上维护总线协议错误的计数

-   指向用于识别数据的驱动程序分配的缓冲区的指针

    类驱动程序必须从缓存对齐的非分页池为返回的有用数据分配内存。 有关为驱动程序缓冲区分配内存的详细信息，请参阅 [分配系统空间内存](../kernel/allocating-system-space-memory.md)。

-   驱动程序确定的 **SrbFlags** 的默认值，该类驱动程序在 SRBs 中设置这些值

-   指向后备链表列表标头的指针（如果驱动程序为它分配的 SRBs 设置后备链表列表）

    有关详细信息，请参阅 [使用后备链表列表](../kernel/using-lookaside-lists.md) 。

-   用于分页操作和错误恢复操作的请求（如存储类驱动程序的 ReleaseQueue 例程执行的操作）以及错误恢复操作 (（如 [存储类驱动程序的例程](storage-class-driver-s-releasequeue-routine.md) 执行的操作），指向 IRP 和分配并保留的 SRB 分配和保留的指针) 

-   一个指针，指向从 HBA 收集的端口驱动程序的 [**存储 \_ 适配器 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor) 和 [**存储 \_ 设备 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor) 数据

    有关类驱动程序如何获取和使用此数据的信息，请参阅 [存储类驱动程序的 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)。

-   指示上一个和当前 PnP 状态的标志，用于管理设备上状态之间的转换

-   一个标志，用于指示当前设备电源状态，以避免额外的处理冗余的电源请求

-   设备上的系统分页文件（如果有）的计数，基于驱动程序收到的寻呼通知请求 (IRP \_ MJ \_ PNP with [**irp \_ MN \_ 设备 \_ 使用 \_ 通知**](../kernel/irp-mn-device-usage-notification.md)) 

存储类驱动程序无法通过存储端口驱动程序向其设备发送请求，而不使用由 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack) 返回的设备对象指针，并且由驱动程序的 *AddDevice* 例程存储在设备扩展中。

 

