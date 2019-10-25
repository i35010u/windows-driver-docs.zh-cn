---
title: 存储类驱动程序的 GetDescriptor 例程
description: 存储类驱动程序的 GetDescriptor 例程
ms.assetid: d1ddcfe8-f276-4e45-82b7-0f07f0526c71
keywords:
- GetDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2974409fb82fc47da579ccf2eb342a2c43ae645
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844747"
---
# <a name="storage-class-drivers-getdescriptor-routine"></a>存储类驱动程序的 GetDescriptor 例程


## <span id="ddk_storage_class_drivers_getdescriptor_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GETDESCRIPTOR_ROUTINE_KG"></span>


对于数据传输操作，存储类驱动程序需要与每个 HBA 的配置信息，驱动其设备所连接到的总线。 若要获取此信息，类驱动程序需要调用内部*GetDescriptor*例程，或在其*StartDevice*例程中实现相同的功能。 （有关*StartDevice*的信息，请参阅[在存储类驱动程序中处理 PnP 开始](handling-pnp-start-in-a-storage-class-driver.md)。）

*GetDescriptor*例程生成并设置查询属性请求（[**IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)与[**IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)），以便端口驱动程序检索设备和类驱动程序在其设备扩展中存储的适配器描述符。 类驱动程序还可以根据返回的描述符数据在设备扩展中设置驱动程序写入器确定的标志。

类驱动程序将检查返回的[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)数据来确定设备功能（scsi 查询数据或非 scsi 等效项）（如 scsi 设备类型），无论设备的媒体（如果有）是否可移动（**RemovableMedia**）、设备是否支持多个未处理的命令（**CommandQueueing**）和各种 ID 字符串。 类驱动程序将检查返回的[**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)数据来确定适配器功能，其中包括：

-   特定 HBA 可以在单个操作中传输的最大字节数（**MaximumTransferLength**）。

-   如果 HBA 可以传输非连续物理页面支持的缓冲数据（换言之，如果它支持散点/集合），则每个传输操作（**MaximumPhysicalPages**）每个缓存可管理的非连续物理页面数。

-   HBA 对传输的对齐要求，因此类驱动程序可以正确设置其设备对象（**AlignmentMask**）中的**AlignmentRequirement**字段。

    通过请求发送[**IOCTL\_SCSI\_\_通过**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)请求的应用程序也可能使用此字段。

    有关在设备对象中设置**AlignmentRequirement**的详细信息，请参阅[初始化设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/initializing-a-device-object)。

-   HBA 是否支持 SCSI 标记的排队和/或每个逻辑单元的内部队列（**CommandQueueing**）。

-   HBA 是否支持同步传输（**AcceleratedTransfer**）。

-   HBA 是否在内部缓存数据（**CachesData**）。

类驱动程序应将此信息存储在 FDO 的设备扩展中，以便其调度例程能够确保发送到存储端口驱动程序的所有请求都符合底层 HBA 的大小、物理中断数和对齐要求。 有关类驱动程序调度例程的详细信息，请参阅[存储类驱动程序的调度例程](storage-class-driver-s-dispatch-routines.md)。 有关设置设备扩展的详细信息，请参阅[设置存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)。

 

 




