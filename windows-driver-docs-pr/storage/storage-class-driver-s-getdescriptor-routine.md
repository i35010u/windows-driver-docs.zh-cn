---
title: 存储类驱动程序的 GetDescriptor 例程
description: 存储类驱动程序的 GetDescriptor 例程
ms.assetid: d1ddcfe8-f276-4e45-82b7-0f07f0526c71
keywords:
- GetDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d351338b02dcf58615dcc453e4b260b51391ecda
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189433"
---
# <a name="storage-class-drivers-getdescriptor-routine"></a>存储类驱动程序的 GetDescriptor 例程


## <span id="ddk_storage_class_drivers_getdescriptor_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GETDESCRIPTOR_ROUTINE_KG"></span>


对于数据传输操作，存储类驱动程序需要与每个 HBA 的配置信息，驱动其设备所连接到的总线。 若要获取此信息，类驱动程序需要调用内部 *GetDescriptor* 例程，或在其 *StartDevice* 例程中实现相同的功能。  (有关 *StartDevice*的信息，请参阅 [在存储类驱动程序中处理 PnP 启动](handling-pnp-start-in-a-storage-class-driver.md)) 

*GetDescriptor*例程生成并设置 ([**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)和[**IOCTL \_ 存储 \_ 查询 \_ 属性**](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)的查询属性请求) ，以使端口驱动程序检索类驱动程序在其设备扩展中存储的设备和适配器描述符。 类驱动程序还可以根据返回的描述符数据在设备扩展中设置驱动程序写入器确定的标志。

类驱动程序将检查返回的 [**存储 \_ 设备 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor) 数据，以确定设备功能 (scsi 查询数据或非 SCSI 等效) （如 scsi 设备类型）、设备媒体是否 () 如果可移动 (**RemovableMedia**) ，无论设备是否支持 **CommandQueueing** (的多个未处理命令以及各种 ID 字符串。 类驱动程序将检查返回的 [**存储 \_ 适配器 \_ 描述符**](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor) 数据，以确定适配器功能，其中包括：

-    (**MaximumTransferLength**) ，特定 HBA 可以在单个操作中传输的最大字节数。

-   如果 HBA 可以传输非连续物理页面支持的缓冲数据 (换言之，如果它支持散点/集合) ，则每个传输操作 (**MaximumPhysicalPages**) 每个缓冲区可以管理的非连续物理页数。

-   HBA 对传输的对齐要求使类驱动程序能够正确地将其设备对象中的 **AlignmentRequirement** 字段设置 (**AlignmentMask**) 。

    通过请求发送 [**IOCTL \_ SCSI \_ PASS \_ **](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) 的应用程序也可能使用此字段。

    有关在设备对象中设置 **AlignmentRequirement** 的详细信息，请参阅 [初始化设备对象](../kernel/initializing-a-device-object.md)。

-   HBA 是否支持 SCSI 标记排队和/或按逻辑单元的内部队列 (**CommandQueueing**) 。

-   HBA 是否支持同步传输 (**AcceleratedTransfer**) 。

-   HBA 是否在内部缓存数据 (**CachesData**) 。

类驱动程序应将此信息存储在 FDO 的设备扩展中，以便其调度例程能够确保发送到存储端口驱动程序的所有请求都符合底层 HBA 的大小、物理中断数和对齐要求。 有关类驱动程序调度例程的详细信息，请参阅 [存储类驱动程序的调度例程](storage-class-driver-s-dispatch-routines.md)。 有关设置设备扩展的详细信息，请参阅 [设置存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)。

 

