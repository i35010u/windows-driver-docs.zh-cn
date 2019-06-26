---
title: MPIO\_路径\_信息 WMI 类
description: MPIO\_路径\_信息 WMI 类
ms.assetid: fd6311c5-2d98-4a3a-beb9-54f3a84be8eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e89093533c2a15f215d787e97fc0d91e983670ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386148"
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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_路径\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_path_information)数据结构。 没有与此 WMI 类相关联的方法。

 

 





