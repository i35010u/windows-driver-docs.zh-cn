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
ms.openlocfilehash: 2ee66f69ae2845b7c560aad7ab78e37b5d8149ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842611"
---
# <a name="setting-up-a-storage-class-drivers-device-extension"></a>设置存储类驱动程序的设备扩展


## <span id="ddk_setting_up_a_storage_class_drivers_device_extension_kg"></span><span id="DDK_SETTING_UP_A_STORAGE_CLASS_DRIVERS_DEVICE_EXTENSION_KG"></span>


在存储类驱动程序所创建的每个设备对象的[设备扩展](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-extensions)中，该驱动程序为其用于管理设备的 i/o 请求的任何驱动程序确定的数据（如指向传递到[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)的 PDO 的指针）提供存储。指向由[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)返回的设备对象的指针、指向其自己的设备对象的返回指针等。

大多数存储类驱动程序还为以下信息提供存储：

-   特定于设备类型的超时值

    类驱动程序可以在它发送到端口驱动程序的 SRBs 中传递超时值，这会导致 SRB\_函数\_通过代表每个类驱动程序执行\_SCSI 请求（请参阅[**scsi\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)）。 如果端口驱动程序将请求发送到基础驱动程序并在请求完成后超过指定的超时时间间隔，则端口驱动程序将返回 SRB，并将其**SrbStatus**成员设置为 SRB\_状态\_超时负值.

-   指向类驱动程序的错误处理例程的指针

    有关存储类驱动程序中的错误处理的详细信息，请参阅[存储类驱动程序的 IoCompletion 例程](storage-class-driver-s-iocompletion-routines.md)。

-   驱动程序在设备上维护总线协议错误的计数

-   指向用于识别数据的驱动程序分配的缓冲区的指针

    类驱动程序必须从缓存对齐的非分页池为返回的有用数据分配内存。 有关为驱动程序缓冲区分配内存的详细信息，请参阅[分配系统空间内存](https://docs.microsoft.com/windows-hardware/drivers/kernel/allocating-system-space-memory)。

-   驱动程序确定的**SrbFlags**的默认值，该类驱动程序在 SRBs 中设置这些值

-   指向后备链表列表标头的指针（如果驱动程序为它分配的 SRBs 设置后备链表列表）

    有关详细信息，请参阅[使用后备链表列表](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-lookaside-lists)。

-   用于分页操作以及错误恢复操作（如[存储类驱动程序的 ReleaseQueue 例程](storage-class-driver-s-releasequeue-routine.md)执行的请求）的请求（即使是在内存不足的情况下），用于为必须成功的请求分配并保留的 SRB 的指针

-   指向[**存储\_适配器的指针\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)和[**存储\_设备\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)数据（从 HBA 收集的端口驱动程序）

    有关类驱动程序如何获取和使用此数据的信息，请参阅[存储类驱动程序的 GetDescriptor 例程](storage-class-driver-s-getdescriptor-routine.md)。

-   指示上一个和当前 PnP 状态的标志，用于管理设备上状态之间的转换

-   一个标志，用于指示当前设备电源状态，以避免额外的处理冗余的电源请求

-   设备上的系统分页文件（如果有）的计数，基于驱动程序收到的寻呼通知请求（IRP\_MJ\_PNP 与[**IRP\_MN\_设备\_使用情况\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)）

存储类驱动程序无法通过存储端口驱动程序向其设备发送请求，而不使用由[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)返回的设备对象指针，并且由驱动程序的*AddDevice*存储在设备扩展中。例程.

 

 




