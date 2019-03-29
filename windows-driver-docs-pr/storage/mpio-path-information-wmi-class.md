---
title: MPIO\_路径\_信息 WMI 类
description: MPIO\_路径\_信息 WMI 类
ms.assetid: fd6311c5-2d98-4a3a-beb9-54f3a84be8eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 22acc36bca41dcb6173b5551c6ae7dffc5fb267c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349608"
---
# <a name="mpiopathinformation-wmi-class"></a>MPIO\_路径\_信息 WMI 类


WMI 客户端使用 MPIO\_路径\_信息 WMI 类来查询有关与 MPIO 磁盘相关联的所有路径的信息的 MPIO 驱动程序。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_路径\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff562441)数据结构。 没有与此 WMI 类相关联的方法。

 

 





