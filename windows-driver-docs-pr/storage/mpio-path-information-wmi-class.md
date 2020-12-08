---
title: MPIO \_ 路径 \_ 信息 WMI 类
description: MPIO \_ 路径 \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 19fda9a93d23d965a790d85310dbeeaa3f954e4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811557"
---
# <a name="mpio_path_information-wmi-class"></a>MPIO \_ 路径 \_ 信息 WMI 类


WMI 客户端使用 MPIO \_ 路径 \_ 信息 WMI 类来查询 mpio 驱动程序，以获取与 MPIO 磁盘关联的所有路径的相关信息。

```cpp
class MPIO_PATH_INFORMATION
{

    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Number of paths to the device.
    //
    [WmiDataId(1),
     read,
     Description("Number of Paths in use") : amended
    ] uint32 NumberPaths;

    //
    // Pad for data alignment.
    //
    [WmiDataId(2),
     read,
     Description("Pad for ULONGLONG Alignment.") : amended
    ] uint32 Pad;

    //
    // Array containing each path's information.
    // Note that each of these are ULONGLONG aligned.
    //
    [WmiDataId(3),
     read,
     Description("Array of Adapter/Path Information.") : amended,
     WmiSizeIs("NumberPaths")
    ] MPIO_ADAPTER_INFORMATION PathList[];

};
```

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ 路径 \_ 信息**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_path_information) 数据结构。 没有与此 WMI 类相关联的方法。

 

