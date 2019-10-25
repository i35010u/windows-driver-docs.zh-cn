---
title: 控制设备访问权限
description: 控制设备访问权限
ms.assetid: b5e562ad-573b-4b0f-9d85-2410fda16e4e
keywords:
- 设备对象 WDK 内核，安全性
- 安全 WDK 设备对象
- 设备访问控制 WDK 内核
- 非 WDM 驱动程序设备访问 WDK 内核
- 安全描述符 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b888be585678f8ca1877d527a5369fb94eef767b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828511"
---
# <a name="controlling-device-access"></a>控制设备访问权限





对设备的访问由安全描述符（及其包含的 ACL）控制。 设备对象的安全描述符可以在创建设备对象时指定，也可以在注册表中设置。

### <a name="controlling-device-access-for-wdm-drivers"></a>控制 WDM 驱动程序的设备访问

当 WDM 驱动程序（而不是特定总线驱动程序）创建设备对象时，即插即用管理器会确定该设备的安全描述符。 运算顺序如下所示。

1.  PnP 管理器调用驱动程序的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程。

2.  驱动程序的*AddDevice*例程调用[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)来创建设备对象并将其附加到设备对象堆栈。

3.  PnP 管理器更新新创建的设备对象的安全描述符。

对于 WDM 驱动程序，PnP 管理器会确定设备对象的安全描述符，如下所示。

1.  如果设备在注册表中具有安全描述符设置，则会将其应用到设备堆栈中的每个对象。

2.  否则，如果设备的安装类在注册表中具有安全描述符设置，则会将其应用到设备堆栈中的每个对象。

3.  否则，PnP 管理器保留每个对象的默认安全描述符不变。 在这种情况下，堆栈的默认安全描述符由 PDO 的设备类型和设备特征确定。

对于大多数设备类型和特征，默认的安全描述符会向管理员提供完全访问权限（通用\_全部）、读取、写入和执行访问（一般\_读取 |泛型\_写入 |一般\_执行）对其他人的访问权限。

有关如何在注册表中设置设备或设备安装程序类的安全描述符的详细信息，请参阅在[注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)。

如果设备在 raw 模式下运行，则 PnP 管理器无法确定设备对象的安全描述符。 在这种情况下，总线驱动程序必须提供安全描述符;请参阅下文。

### <a name="controlling-device-access-for-wdm-bus-drivers"></a>控制 WDM 总线驱动程序的设备访问

WDM 总线驱动程序必须为可以在 raw 模式下操作的每个设备的 PDO 提供安全描述符。 使用[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)创建具有安全描述符的设备对象。

如果总线驱动程序未在 raw 模式下操作设备，则不需要提供安全描述符。 PnP 管理器会确定安全描述符，如上所述。 如果总线驱动程序必须确保其 PDOs 具有比默认描述符更严格的安全设置，则它可以提供安全描述符。 由总线驱动程序指定的任何描述符被注册表中的设置覆盖。

有关创建设备对象的详细信息，请参阅[创建设备对象](creating-a-device-object.md)。

### <a name="controlling-device-access-for-non-wdm-drivers"></a>控制非 WDM 驱动程序的设备访问

非 WDM 驱动程序必须为其创建的任何命名设备对象指定默认安全描述符和类 GUID。

使用**IoCreateDeviceSecure**例程创建命名设备对象，并为该设备指定默认安全描述符和类 GUID。 安全描述符是在 SDDL 的子集中指定的。 有关详细信息，请参阅[适用于设备对象的 SDDL](sddl-for-device-objects.md)。

系统将覆盖默认安全描述符，其中包含指定类 GUID 的注册表中的任何安全设置。 驱动程序必须为设备指定其自己的唯一 GUID。 使用 Guidgen.exe 工具生成唯一 GUID。 （Guidgen.exe 包含在 Microsoft Windows SDK 中。）

 

 




