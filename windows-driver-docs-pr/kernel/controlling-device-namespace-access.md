---
title: 控制设备命名空间访问权限
description: 控制设备命名空间访问权限
keywords:
- 设备对象 WDK 内核，安全性
- 安全 WDK 设备对象
- 设备命名空间访问 WDK 内核
- 命名空间 WDK 设备对象
- 文件打开请求 WDK 设备对象
- 打开请求 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a06c4b6e97fc1b5dee191755788c7d09aa13015c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830411"
---
# <a name="controlling-device-namespace-access"></a>控制设备命名空间访问权限





在 Windows 驱动模型 (WDM) ，每个设备对象都有一个关联的 *命名空间*。 设备命名空间中的名称是以设备名称开头的路径。 对于名为 " \\ *device* \\ *DeviceName*" 的设备，其命名空间包含 " \\ *device* \\ *DeviceName* \\ *FileName*" 格式的任何名称。 对于文件系统 (， *FileName* 是文件系统上文件的实际名称。 ) 

WDM 驱动程序接收设备命名空间中所有名称的打开请求。 驱动程序会将 "设备 DeviceName" 的打开请求视为 \\ *Device* \\ *DeviceName* 设备对象本身的打开请求。 如果驱动程序在设备的命名空间中实现对打开请求的支持，则它会将 " \\ *设备* \\ *DeviceName* \\ *FileName*" 的打开请求作为设备对象命名空间中的 "文件" 的打开状态， (其中设备的 "文件" 概念由驱动程序确定) 。

大多数驱动程序不支持将打开操作引入设备的命名空间，但所有驱动程序都必须提供安全检查，以防止未经授权访问设备的命名空间。 默认情况下，在设备的命名空间内对文件打开请求进行安全检查， (例如，" \\ *device* \\ *DeviceName* \\ *FileName*" ) 完全保留到驱动程序中，操作系统不检查设备对象 ACL。

如果设置了设备对象的文件 \_ 设备 \_ 安全 \_ 打开特性，则系统会将设备对象的安全描述符应用到设备命名空间中的所有文件打开请求。 驱动程序可 \_ \_ \_ 在创建具有 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 或 [**IOCREATEDEVICESECURE**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)的设备对象时设置文件设备安全打开。 对于 WDM 驱动程序， \_ \_ \_ 还可以在注册表中设置文件设备安全打开。 还可以在注册表中为 **IoCreateDeviceSecure** 创建的非 WDM 驱动程序的设备对象设置。 有关在注册表中设置设备对象属性（例如设备特征）的详细信息，请参阅在 [注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)。 有关设备特征的详细信息，请参阅 [指定设备特征](specifying-device-characteristics.md)。

不支持命名空间的设备的驱动程序必须使用以下两种方法之一来确保正确处理设备命名空间中的文件打开请求：

-   驱动程序的设备对象具有文件 \_ 设备 \_ 安全 \_ 打开设备特征集。 然后，该驱动程序可以将任何打开的请求作为设备对象的打开请求处理到设备的命名空间中。

-   驱动程序可能会导致指定 IrpSp 参数的任何 [**IRP \_ MJ \_ CREATE**](./irp-mj-create.md)请求失败，其长度为非零值。 **&gt; &gt;** 在这种情况下，设备的打开请求受系统的 ACL 检查的限制，而设备命名空间内的所有文件打开请求都将失败。 支持独占打开 (驱动程序必须使用此选项。 ) 

支持命名空间的设备的驱动程序还可以使用两种方法来确保将文件打开的请求固定到设备的命名空间中：

-   驱动程序的设备对象具有文件 \_ 设备 \_ 安全 \_ 打开设备特征集。 这可确保设备的安全设置统一应用于设备的命名空间。  (驱动程序负责在其 [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 回调函数中实现命名空间支持。 ) 

-   驱动程序在其 *DispatchCreate* 例程中检查文件名的任何 acl。 即使在这种情况下，驱动程序也应该设置文件 \_ 设备 \_ 安全 \_ 开放特征，除非打开到设备的命名空间的安全设置比设备对象更弱。 )  (

\_ \_ \_ 在堆栈顶部检查 "文件设备安全打开" 特性，因此在附加后，筛选器设备对象必须复制下一个较低设备对象的 **特征** 成员。

 

