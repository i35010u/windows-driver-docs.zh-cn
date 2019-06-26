---
title: MPIO\_获取\_描述符 WMI 类
description: MPIO\_获取\_描述符 WMI 类
ms.assetid: 6d48c0b5-c20f-4017-aae5-0b00fa5de18d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4263296f8962633cce9a0305e2dbdad7474f28d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386156"
---
# <a name="mpiogetdescriptor-wmi-class"></a>MPIO\_获取\_描述符 WMI 类


WMI 客户端使用 MPIO\_获取\_描述符 WMI 类来查询为 MPIO 磁盘设备路径配对 MPIO。

```cpp
class MPIO_GET_DESCRIPTOR
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Number of instances of this device via different paths.
    //
    [WmiDataId(1),
     read,
     Description("Number of Port Objects backing the device.") : amended
    ] uint32 NumberPdos;

    //
    // Device Name (i.e. MPIODiskN)
    //
    [WmiDataId(2),
     read,
     MaxLen(63),
     Description("Name of Device.") : amended
    ] string DeviceName;

    //
    // Array of device-path pair that form the instances of this device.
    //
    [WmiDataId(3),
     read,
     Description("Array of Information classes describing the real device.") : amended,
     WmiSizeIs("NumberPdos")
    ] PDO_INFORMATION PdoInformation[];
};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_获取\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_mpio_get_descriptor)数据结构。 没有与此 WMI 类相关联的方法。

 

 





