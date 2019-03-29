---
title: 存储驱动程序和设备对象
description: 存储驱动程序和设备对象
ms.assetid: dbadebe6-b2ae-4dc2-837b-5ca9634d45d0
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90e12270b8ba39446bf7e4342c01077158d81a0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566220"
---
# <a name="storage-drivers-and-device-objects"></a>存储驱动程序和设备对象


## <span id="ddk_storage_drivers_and_device_objects_kg"></span><span id="DDK_STORAGE_DRIVERS_AND_DEVICE_OBJECTS_KG"></span>


存储设备堆栈包含，由参与处理 I/O 来在系统上的存储设备的驱动程序创建的设备对象的树。 此树的根是一个功能的设备对象 (FDO) 存储适配器或另一个驱动程序堆栈与存储堆栈集成。 此树的叶是供文件系统和用户模式应用程序使用的设备对象。

像任何即插即用驱动程序、 存储类或存储筛选器驱动程序将自身添加到其 AddDevice 例程中的树通过创建设备对象与**IoCreateDevice**并将其附加到使用设备堆栈**IoAttachDeviceToDeviceStack**，由即插即用管理器在初始化时使用设备对象的指针传递给驱动程序的 AddDevice 例程。 **IoAttachDeviceToDeviceStack**将新的设备对象附加到当前设备堆栈的顶部。

磁带 miniclass、 媒体更换器 miniclass 或 SCSI 微型端口驱动程序不需要创建一个设备对象并将其附加到设备堆栈。 相反，系统提供磁带类、 转换器类或 SCSI 端口驱动程序处理代表调用 miniclass/微型端口驱动程序例程来收集数据，创建设备对象所需 miniclass/微型端口，这些任务。

存储端口驱动程序创建的文件类型的物理设备对象 (PDOs)\_设备\_大容量\_存储。 磁盘类、 CD-ROM 类、 磁带类和转换器类驱动程序创建的类型文件 FDOs\_设备\_磁盘、 文件\_设备\_CD\_ROM、 文件\_设备\_磁带，和文件\_设备\_换带机分别。

有关设计即插即用驱动程序的信息，请参阅[即插即用驱动程序设计指南](https://msdn.microsoft.com/library/windows/hardware/ff559623)。 有关 PnP 相关信息 **Io * * * Xxx*例程，请参阅[插例程](https://msdn.microsoft.com/library/windows/hardware/ff558809)。

 

 




