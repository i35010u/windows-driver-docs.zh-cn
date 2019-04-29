---
title: MPIO\_DSM\_路径 WMI 类
description: MPIO\_DSM\_路径 WMI 类
ms.assetid: 4f8d7fb0-2b9a-44dc-bb87-f70285f1b47c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1a861a667cc0c73ec437c4d54aa977bb67b18f7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391391"
---
# <a name="mpiodsmpath-wmi-class"></a>MPIO\_DSM\_路径 WMI 类


MPIO 发布 MPIO\_DSM\_路径\_V2 WMI 类但需要进行注册，GUID 和处理其实现的 DSM。 MPIO 驱动程序使用 MPIO\_DSM\_路径\_V2 WMI 类，以报告的 DSM 标识路径 ID。

```cpp
class MPIO_DSM_Path
{

    //
    // Unique identifier to distinguish paths known to the DSM.
    // This is what is returned to MPIO during DsmSetDeviceInfo.
    //
    [WmiDataId(1),
     Description("DSM Path Id") : amended
    ]
    uint64 DsmPathId;

    //
    // Reserved.
    //
    [WmiDataId(2),
     Description("Reserved field") : amended
    ]
    uint64 Reserved;

    //
    // Value that determines which path the DSM picks if the load balance is
    // Weighted Paths.
    //
    [WmiDataId(3),
     Description("Weight assigned to the path") : amended
    ]
    uint32 PathWeight;

    //
    // Flag to indicate if this is a primary path.
    //
    [WmiDataId(4),
     Description("Flag set to TRUE if the path is a primary path. Else FALSE.") : amended
    ]
    uint32 PrimaryPath;
};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_DSM\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff562382)数据结构。 没有与此 WMI 类相关联的方法。

 

 





