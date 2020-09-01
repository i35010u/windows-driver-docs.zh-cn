---
title: MPIO \_ 路径 \_ 信息 WMI 类
description: MPIO \_ 路径 \_ 信息 WMI 类
ms.assetid: fd6311c5-2d98-4a3a-beb9-54f3a84be8eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 15d356fab1ffcf322d27c9162893d854ba50d4ae
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184205"
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

 

