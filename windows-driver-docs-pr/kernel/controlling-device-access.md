---
title: 控制设备访问权限
description: 控制设备访问权限
ms.assetid: b5e562ad-573b-4b0f-9d85-2410fda16e4e
keywords:
- 设备对象 WDK 内核安全性
- 安全 WDK 设备对象
- 设备访问控件 WDK 内核
- 非 WDM 驱动程序设备访问 WDK 内核
- 安全描述符 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3d54ab5ccbfe4537b2ce651edfad5fde3ecdc87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377204"
---
# <a name="controlling-device-access"></a>控制设备访问权限





对设备的访问控制安全说明符 （和它包含 ACL）。 创建，或在注册表中设置的设备对象时，可以指定一个设备对象的安全描述符。

### <a name="controlling-device-access-for-wdm-drivers"></a>用于 WDM 驱动程序来控制设备访问权限

当 WDM 驱动程序 （而不是特定的总线驱动程序） 创建设备对象时，插管理器确定设备的安全描述符。 操作的顺序是按如下所示。

1.  PnP 管理器会调用驱动程序的[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。

2.  在驱动程序*AddDevice*例程调用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)以创建设备对象并将其附加到设备对象堆栈。

3.  即插即用 manager 更新新创建的设备对象的安全描述符。

WDM 驱动程序，即插即用管理器确定设备对象的安全描述符，如下所示。

1.  如果设备在注册表中具有安全描述符设置，它将应用于设备堆栈中的每个对象。

2.  否则，如果设备的安装程序类在注册表中具有安全描述符设置，它将应用于设备堆栈中的每个对象。

3.  否则，即插即用管理器将保持不变的每个对象的默认安全描述符。 在这种情况下，按设备类型和设备特征的 PDO 确定堆栈的默认安全描述符。

对于大多数设备类型和特征的默认安全描述符授予完全访问权限 (泛型\_所有) 管理员，并读取、 写入和执行访问权限 (通用\_读取 |泛型\_编写 |泛型\_EXECUTE) 对其他人访问。

有关如何在注册表中设置安全描述符为设备或设备安装程序类的详细信息，请参阅[在注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)。

如果设备在原始模式下操作，即插即用管理器无法确定的设备对象的安全描述符。 在这种情况下，总线驱动程序必须提供的安全描述符;请参阅下文。

### <a name="controlling-device-access-for-wdm-bus-drivers"></a>用于 WDM 总线驱动程序来控制设备访问权限

WDM 总线驱动程序必须提供的是 PDO 可以在 raw 模式中处理每个设备的安全描述符。 使用[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)带有安全描述符创建设备对象。

如果总线驱动程序不能运行在 raw 模式的设备，然后它不是需要提供的安全描述符。 PnP 管理器确定的安全描述符，如上文所述。 如果它必须确保其 PDOs 具有比默认描述符较严格的安全设置，总线驱动程序可以提供的安全描述符。 由总线驱动程序指定任何描述符由注册表中的设置重写。

有关创建设备对象的详细信息，请参阅[创建一个设备对象](creating-a-device-object.md)。

### <a name="controlling-device-access-for-non-wdm-drivers"></a>用于非 WDM 驱动程序来控制设备访问权限

非 WDM 驱动程序必须指定默认安全描述符和他们创建的任何命名的设备对象的类 GUID。

使用**IoCreateDeviceSecure**例程来创建指定的设备对象和指定的默认安全描述符，并为该设备类 GUID。 中的 SDDL 子集指定安全描述符。 有关详细信息，请参阅[设备对象的 SDDL](sddl-for-device-objects.md)。

系统将重写与指定的类 GUID 的注册表中的任何安全设置的默认安全描述符。 该驱动程序必须指定其自己的设备的唯一 GUID。 使用 GuidGen 工具生成的唯一 GUID。 （GuidGen 包含在 Microsoft Windows SDK 中）。

 

 




