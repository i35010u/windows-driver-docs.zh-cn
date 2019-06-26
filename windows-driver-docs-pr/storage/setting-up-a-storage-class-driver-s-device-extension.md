---
title: 设置存储类驱动程序的设备扩展
description: 设置存储类驱动程序的设备扩展
ms.assetid: 9d050d23-39c0-406e-9f4b-2e95d388f5cf
keywords:
- 存储类驱动程序 WDK，设备扩展
- 类驱动程序 WDK 存储设备扩展
- 设备扩展 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d06b124375a8b9fbc41ad95fc2e9c98c94179f28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363946"
---
# <a name="setting-up-a-storage-class-drivers-device-extension"></a>设置存储类驱动程序的设备扩展


## <span id="ddk_setting_up_a_storage_class_drivers_device_extension_kg"></span><span id="DDK_SETTING_UP_A_STORAGE_CLASS_DRIVERS_DEVICE_EXTENSION_KG"></span>


在中[设备扩展](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-extensions)的每个创建的存储类驱动程序的设备对象，该驱动程序提供了存储任何驱动程序确定的数据，它使用管理 I/O 请求的设备，如 PDO 指向传递给[ **AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)，指向返回的设备对象指针[ **IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)，指向其自己的后指针设备对象等。

大多数存储类驱动程序还提供存储以下信息：

-   特定于设备的类型的超时值

    在类驱动程序可以在它发送到端口驱动程序，其计时 SRB Srb 中传递的超时值\_函数\_EXECUTE\_SCSI 请求 (请参阅[ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)) 代表每个类驱动程序。 端口驱动程序将返回与 SRB 及其**SrbStatus**成员设置为 SRB\_状态\_超时如果端口驱动程序将请求中发送到基础驱动程序和在请求完成时之间的间隔超过了指定的超时值。

-   指向类驱动程序的错误处理例程的指针

    请参阅[存储类驱动程序 IoCompletion 例程](storage-class-driver-s-iocompletion-routines.md)有关存储类驱动程序中的错误处理的详细信息。

-   驱动程序保持在设备上的总线协议错误的计数

-   指向检测数据驱动程序分配的缓冲区的指针

    从缓存对齐，非分页池，类驱动程序必须为返回有意义的数据分配内存。 有关驱动程序缓冲区分配内存的详细信息，请参阅[分配系统空间内存](https://docs.microsoft.com/windows-hardware/drivers/kernel/allocating-system-space-memory)。

-   驱动程序确定的默认值**SrbFlags**中 Srb 设置类驱动程序

-   如果该驱动程序设置后备链列表 Srb 为它的后备链列表标头的指针分配

    请参阅[使用后备链列表](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-lookaside-lists)有关详细信息。

-   指向 IRP 和 SRB 分配和保留的请求必须成功甚至是在低内存条件，但是对于分页操作以及错误恢复操作 (例如那些由执行[存储类驱动程序 ReleaseQueue例程](storage-class-driver-s-releasequeue-routine.md))

-   一个指向[**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)并[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_device_descriptor)端口驱动程序从 HBA 收集的数据

    有关类驱动程序如何获取和使用此数据的信息，请参阅[存储类驱动程序 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)。

-   这些标志指示以前和当前即插即用状态，来管理设备上的状态之间转换

-   一个标志，指示当前的设备电源状态，以避免额外工作地处理冗余电源请求

-   计数系统分页文件，如果有的话，在设备上，基于由驱动程序接收到寻呼通知请求 (IRP\_MJ\_与 PNP [ **IRP\_MN\_设备\_使用情况\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification))

存储类驱动程序不能将请求发送到存储端口驱动程序通过其设备而无需使用返回的设备对象指针[ **IoAttachDeviceToDeviceStack** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)并存储在由驱动程序的设备扩展*AddDevice*例程。

 

 




