---
title: 存储类驱动程序的 GetDescriptor 例程
description: 存储类驱动程序的 GetDescriptor 例程
ms.assetid: d1ddcfe8-f276-4e45-82b7-0f07f0526c71
keywords:
- GetDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee0b0f5fa489d944f94e7a068340d3ebd60fd29b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368201"
---
# <a name="storage-class-drivers-getdescriptor-routine"></a>存储类驱动程序的 GetDescriptor 例程


## <span id="ddk_storage_class_drivers_getdescriptor_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_GETDESCRIPTOR_ROUTINE_KG"></span>


对于数据传输操作中，存储类驱动程序需要有关每个 HBA 驱动其设备连接到总线的配置信息。 若要获取此信息，请类驱动程序可以调用内部*GetDescriptor*例程或实现中相同的功能及其*StartDevice*例程。 (有关*StartDevice*，请参阅[存储类驱动程序中处理即插即用启动](handling-pnp-start-in-a-storage-class-driver.md)。)

一个*GetDescriptor*例程生成，并设置查询属性请求 ([**IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)与[**IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)) 端口驱动程序检索的类驱动程序存储在其设备的设备和适配器描述符扩展插件。 类驱动程序还可能会根据返回的描述符数据的设备扩展中设置确定驱动程序编写器的标志。

返回的类驱动程序将检查[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)数据，如确定设备功能 （SCSI 查询数据或非 SCSI 等效项）SCSI 设备类型，无论设备的介质 （如果有） 是可移动 (**RemovableMedia**)，无论设备是否支持多个未完成的命令 (**CommandQueueing**)，和各种 ID字符串。 返回的类驱动程序将检查[**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)数据来确定适配器功能，包括：

-   最大特定 HBA 可以在单个操作中传输的字节数 (**MaximumTransferLength**)。

-   如果传输 HBA 可以缓冲的数据支持的非连续的物理页面 （换句话说，如果它支持散播-聚集），多少不连续的物理页，每次可缓存它可以管理，每个传输操作 (**MaximumPhysicalPages**).

-   HBA 的对齐要求的传输，因此可以正确设置的类驱动程序**AlignmentRequirement**字段中其设备对象 (**AlignmentMask**)。

    发送的应用程序[ **IOCTL\_SCSI\_传递\_THROUGH** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)请求还可以使用此字段。

    有关设置详细信息**AlignmentRequirement**中的设备对象，请参阅[初始化设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/initializing-a-device-object)。

-   HBA 支持 SCSI 标记队列和/或逻辑单元内部队列 (**CommandQueueing**)。

-   HBA 是否支持同步传输 (**AcceleratedTransfer**)。

-   HBA 在内部缓存的数据是否 (**CachesData**)。

在类驱动程序应 FDO 设备扩展中存储此信息，以便其调度例程可以确保发送到存储端口驱动程序的所有请求都符合大小、 数量的物理分隔线和对齐要求的基础的 HBA。 有关类驱动程序调度例程的详细信息，请参阅[存储类驱动程序调度例程](storage-class-driver-s-dispatch-routines.md)。 有关设置设备扩展的详细信息，请参阅[设置了存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)。

 

 




