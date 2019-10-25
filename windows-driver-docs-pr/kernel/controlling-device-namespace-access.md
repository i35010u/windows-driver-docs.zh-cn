---
title: 控制设备命名空间访问权限
description: 控制设备命名空间访问权限
ms.assetid: e5312297-849f-4b4e-835d-0ce5295c7ce2
keywords:
- 设备对象 WDK 内核，安全性
- 安全 WDK 设备对象
- 设备命名空间访问 WDK 内核
- 命名空间 WDK 设备对象
- 文件打开请求 WDK 设备对象
- 打开请求 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 853039c1268c4456b2ef1eac6ce914651534276f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837048"
---
# <a name="controlling-device-namespace-access"></a>控制设备命名空间访问权限





在 Windows 驱动模型（WDM）中，每个设备对象都有一个关联的*命名空间*。 设备命名空间中的名称是以设备名称开头的路径。 对于名为 "\\*device*\\*DeviceName*" 的设备，其命名空间由 "\\*设备*\\*DeviceName*\\*FileName*" 格式的任意名称组成。 （对于文件系统， *FileName*是文件系统上的文件的实际名称。）

WDM 驱动程序接收设备命名空间中所有名称的打开请求。 驱动程序将 "\\*设备*\\*DeviceName*" 的打开请求作为设备对象本身的开放处理。 如果驱动程序在设备的命名空间中实现对打开请求的支持，则它会将 "\\*设备*\\*DeviceName*\\*FileName*" 的打开请求作为设备对象命名空间中的 "文件" 打开（其中设备的 "文件" 概念由驱动程序决定）。

大多数驱动程序不支持将打开操作引入设备的命名空间，但所有驱动程序都必须提供安全检查，以防止未经授权访问设备的命名空间。 默认情况下，对设备命名空间内的文件打开请求进行安全检查（例如，"\\*设备*\\*DeviceName*\\*FileName*"）完全由驱动程序使用，不会检查设备对象 ACL操作系统。

如果设备对象的文件\_设备\_SECURE\_开放特征，则系统会将设备对象的安全描述符应用到设备命名空间中的所有文件打开请求。 驱动程序可以在创建[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)或[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)设备对象时将文件\_设备设置\_SECURE\_打开。 对于 WDM 驱动程序，还可以在注册表中设置文件\_设备\_SECURE\_开放。 还可以在注册表中为**IoCreateDeviceSecure**创建的非 WDM 驱动程序的设备对象设置。 有关在注册表中设置设备对象属性（例如设备特征）的详细信息，请参阅在[注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)。 有关设备特征的详细信息，请参阅[指定设备特征](specifying-device-characteristics.md)。

不支持命名空间的设备的驱动程序必须使用以下两种方法之一来确保正确处理设备命名空间中的文件打开请求：

-   驱动程序的设备对象的文件\_设备\_SECURE\_开放设备特征集。 然后，该驱动程序可以将任何打开的请求作为设备对象的打开请求处理到设备的命名空间中。

-   驱动程序可能会失败任何[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)请求，该请求指定长度不为零的**IrpSp&gt;FileObject&gt;FileName**参数。 在这种情况下，设备的打开请求受系统的 ACL 检查的限制，而设备命名空间内的所有文件打开请求都将失败。 （支持独占打开的驱动程序必须使用此选项。）

支持命名空间的设备的驱动程序还可以使用两种方法来确保将文件打开的请求固定到设备的命名空间中：

-   驱动程序的设备对象的文件\_设备\_SECURE\_开放设备特征集。 这可确保设备的安全设置统一应用于设备的命名空间。 （驱动程序负责在其[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)回调函数中实现对命名空间的支持。）

-   驱动程序在其*DispatchCreate*例程中检查文件名的任何 acl。 （在这种情况下，驱动程序应将文件\_设备设置为\_安全\_开放特征，除非打开到设备的命名空间的安全设置比设备对象更弱。）

文件\_设备\_安全\_打开的特性在堆栈顶部进行检查，因此在附加后，筛选器设备对象必须复制下一个较低设备对象的**特征**成员。

 

 




