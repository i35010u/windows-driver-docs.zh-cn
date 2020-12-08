---
title: MPIO \_ 获取 \_ 描述符 WMI 类
description: MPIO \_ 获取 \_ 描述符 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d04c990837d01bf592e543f5a4c1580dda357a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835017"
---
# <a name="mpio_get_descriptor-wmi-class"></a>MPIO \_ 获取 \_ 描述符 WMI 类


WMI 客户端使用 MPIO \_ GET \_ 描述符 WMI 类来查询 mpio 磁盘的设备路径配对。

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

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ 获取 \_ 描述符**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_mpio_get_descriptor) 数据结构。 没有与此 WMI 类相关联的方法。

 

