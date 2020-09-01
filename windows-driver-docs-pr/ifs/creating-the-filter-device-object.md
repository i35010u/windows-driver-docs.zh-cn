---
title: 创建筛选器设备对象
description: 创建筛选器设备对象
ms.assetid: aca9a2ba-8630-4eb3-9312-a0c6454c3e44
keywords:
- 筛选器驱动程序 WDK 文件系统，附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 将筛选器附加到文件系统或卷
- 卷 WDK 文件系统，附加筛选器
- IoCreateDevice
- 筛选 DOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f8dc795678edc2b3c5569e91bd3909c63661b6d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065078"
---
# <a name="creating-the-filter-device-object"></a>创建筛选器设备对象


## <span id="ddk_creating_the_filter_device_object_if"></span><span id="DDK_CREATING_THE_FILTER_DEVICE_OBJECT_IF"></span>


调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 创建要附加到卷或文件系统堆栈的筛选器设备对象，如以下示例中所示：

```cpp
status = IoCreateDevice(
          gFileSpyDriverObject,                     //DriverObject
          sizeof(MYLEGACYFILTER_DEVICE_EXTENSION),  //DeviceExtensionSize
          NULL,                                     //DeviceName
          DeviceObject->DeviceType,                 //DeviceType
          0,                                        //DeviceCharacteristics
          FALSE,                                    //Exclusive
          &newDeviceObject);                        //DeviceObject
```

在上面的代码片段中， *DeviceObject* 是一个指针，指向筛选器设备对象将附加到的目标设备对象; *newDeviceObject* 是指向筛选器设备对象本身的指针。

将 *DeviceExtensionSize* 参数设置为 **sizeof** (MYLEGACYFILTER \_ device \_ extension) 会导致为 \_ \_ 筛选器设备对象分配 MYLEGACYFILTER 设备扩展结构。 新创建的筛选器设备对象的 **DeviceExtension** 成员设置为指向此结构。 文件系统筛选器驱动程序通常为每个筛选器设备对象的设备扩展定义和分配内存。 设备扩展的结构和内容是驱动程序特定的。 但是，在 Microsoft Windows XP 和更高版本中，筛选器驱动程序应该 \_ 为筛选器驱动程序对象定义至少包含以下成员的设备扩展结构：

```cpp
PDEVICE_OBJECT AttachedToDeviceObject;
```

在上述对 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)的调用中，将 *DeviceName* 参数设置为 **NULL** 可指定筛选器设备对象不会命名为。 从不命名筛选器设备对象。 由于筛选器设备对象附加到文件系统或卷驱动程序堆栈，因此为筛选器设备对象指定一个名称将创建系统安全漏洞。

*DeviceType*参数必须始终设置为与目标 (文件系统相同的设备类型或筛选器设备对象所附加到的筛选) 设备对象。 以这种方式传播设备类型非常重要，因为它由 i/o 管理器使用，并可被报告回应用程序。

**注意**   文件系统和文件系统筛选器驱动程序不应将*DeviceType*参数设置为文件 \_ 设备 \_ 文件 \_ 系统。 这不是此参数的有效值。  (文件 \_ 设备 \_ 文件 \_ 系统常量仅适用于定义 FSCTL 代码。 ) 

 

*DeviceType*参数非常重要的另一个原因是，许多筛选器仅附加到某些类型的文件系统。 例如，特定筛选器可能附加到所有本地磁盘文件系统，但不能附加到 CD-ROM 文件系统或远程文件系统。 此类筛选器通过检查文件系统或卷驱动程序堆栈中最顶层设备对象的设备类型来确定文件系统的类型。 在大多数情况下，堆栈中最顶层的设备对象是一个筛选器设备对象。 因此，所有附加的筛选器设备对象具有与基础文件系统或卷设备对象相同的设备类型，这一点非常重要。

 

