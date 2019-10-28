---
title: 存储驱动程序和设备对象
description: 存储驱动程序和设备对象
ms.assetid: dbadebe6-b2ae-4dc2-837b-5ca9634d45d0
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12295a676b489f194b03b118466845b3de3d699b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844484"
---
# <a name="storage-drivers-and-device-objects"></a>存储驱动程序和设备对象


## <span id="ddk_storage_drivers_and_device_objects_kg"></span><span id="DDK_STORAGE_DRIVERS_AND_DEVICE_OBJECTS_KG"></span>


存储设备堆栈包含由驱动程序创建的设备对象树，这些驱动程序由处理系统上存储设备的 i/o 所涉及。 此树的根是存储适配器或与存储堆栈集成的其他驱动程序堆栈的功能设备对象（FDO）。 此树的叶是设备对象，供文件系统和用户模式应用程序使用。

与任何 PnP 驱动程序一样，存储类或存储筛选器驱动程序通过使用**IoCreateDevice**创建设备对象并使用**IoAttachDeviceToDeviceStack**将其附加到设备堆栈，从而将其自身添加到 AddDevice 例程中的树中。一个指针，指向由 PnP 管理器在初始化时传递给驱动程序的 AddDevice 例程的设备对象。 **IoAttachDeviceToDeviceStack**将新设备对象附加到设备堆栈的当前顶部。

创建设备对象并将其附加到设备堆栈时无需使用磁带 miniclass、中转换器 miniclass 或 SCSI 微型端口驱动程序。 相反，系统提供的磁带类、更换器类或 SCSI 端口驱动程序代表 miniclass/微型端口处理这些任务，调用 miniclass/微型端口驱动程序例程来收集创建设备对象所需的数据。

存储端口驱动程序创建文件类型的物理设备对象（PDOs），\_设备\_大容量\_存储。 Disk 类、CD-ROM 类、磁带类和变换器类驱动程序创建 FDOs 类型的文件\_设备\_磁盘、文件\_设备\_CD\_ROM、文件\_设备\_磁带和文件\_设备分别\_变换器。

有关设计 PnP 驱动程序的信息，请参阅[PnP 驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/kernel/pnp-driver-design-guidelines)。 有关与 PnP 相关的 **Io * * Xxx*例程的信息，请参阅[即插即用例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

 

 




