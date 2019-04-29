---
title: 控制设备命名空间访问权限
description: 控制设备命名空间访问权限
ms.assetid: e5312297-849f-4b4e-835d-0ce5295c7ce2
keywords:
- 设备对象 WDK 内核安全性
- 安全 WDK 设备对象
- 设备命名空间访问 WDK 内核
- 命名空间 WDK 设备对象
- 文件打开请求 WDK 设备对象
- 打开请求 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc6396f97175122301d7dcd471c455ba2c02fdc6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369287"
---
# <a name="controlling-device-namespace-access"></a>控制设备命名空间访问权限





在 Windows 驱动程序模型 (WDM) 中，设备的每个对象都有一个关联*命名空间*。 设备的命名空间中的名称是设备的名称开头的路径。 对于名为的设备"\\*设备*\\*DeviceName*"，其命名空间包含窗体的任何名称"\\*设备*\\*DeviceName*\\*FileName*"。 (有关文件系统*文件名*是文件系统上的文件的实际名称。)

WDM 驱动程序接收设备的命名空间中的所有名称打开请求。 驱动程序会将为一个 open 请求"\\*设备*\\*DeviceName*"为已打开的设备对象本身。 如果该驱动程序实现支持打开请求到设备的命名空间，则它将为一个 open 请求"\\*设备*\\*DeviceName* \\ *文件名*"作为"文件"中的设备对象的命名空间 （其中的设备的"文件"这一概念是驱动程序确定） 的开放。

大多数驱动程序不会实现对到设备的命名空间中，打开操作的支持，但所有驱动程序必须提供安全检查，以防止未经授权的访问设备的命名空间。 默认情况下，安全检查的设备的命名空间中的文件打开请求 (例如，"\\*设备*\\*DeviceName* \\ *文件名*") 应完全由驱动程序 — ACL 不会检查操作系统的设备对象。

如果一个设备对象的文件\_设备\_SECURE\_设置打开特征，则系统将设备对象的安全描述符应用到设备的命名空间中的所有文件打开请求。 驱动程序可以设置文件\_设备\_SECURE\_他们创建的设备对象时，打开[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)或[ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)。 对于 WDM 驱动程序文件\_设备\_SECURE\_还可以在注册表中设置打开。 它还可以设置的设备对象的非 WDM 驱动程序创建的注册表中**IoCreateDeviceSecure**。 设置设备对象属性，如设备特征，在注册表中，有关详细信息，请参阅[在注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)。 有关设备特征的详细信息，请参阅[指定设备特征](specifying-device-characteristics.md)。

不支持命名空间的设备的驱动程序必须使用两种方法之一来确保正确处理设备的命名空间中的文件打开请求：

-   驱动程序的设备对象具有该文件\_设备\_SECURE\_打开设备特征集。 驱动程序可以然后视为打开的任何请求到设备的命名空间中的设备对象的打开请求。

-   该驱动程序无法执行任何[ **IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729)指定的请求**IrpSp-&gt;文件对象-&gt;文件名**其长度为非零值的参数。 在这种情况下，打开请求的设备都将受到系统的 ACL 检查，而设备的命名空间内的所有文件打开请求都失败由驱动程序。 （支持排他打开的驱动程序必须使用此选项。）

支持命名空间的设备的驱动程序还可以使用两种方法来保护文件打开请求到设备的命名空间：

-   驱动程序的设备对象具有该文件\_设备\_SECURE\_打开设备特征集。 这可确保设备的安全设置统一应用于设备的命名空间。 (该驱动程序负责实施对中的命名空间的支持及其[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)回调函数。)

-   该驱动程序将检查任何 Acl 中的文件名称及其*DispatchCreate*例程。 (即使在这种情况下，驱动程序应将文件设置\_设备\_SECURE\_打开特征，除非将打开到设备的命名空间中可以具有较弱于设备的对象的安全设置。)

该文件\_设备\_SECURE\_打开特征检查堆栈的顶部，因此必须复制筛选设备对象**特征**之后的下一步下一个设备对象的成员附加。

 

 




