---
title: MPIO \_ DSM \_ 路径 WMI 类
description: MPIO \_ DSM \_ 路径 WMI 类
ms.assetid: 4f8d7fb0-2b9a-44dc-bb87-f70285f1b47c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc666923b9c2bcf03d824875997851f34a80e060
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188931"
---
# <a name="mpio_dsm_path-wmi-class"></a>MPIO \_ DSM \_ 路径 WMI 类


MPIO 发布 MPIO \_ DSM \_ 路径 \_ V2 WMI 类，但要求 DSM 注册 GUID 并处理其实现。 MPIO 驱动程序使用 MPIO \_ dsm \_ 路径 \_ V2 WMI 类来标识 DSM 报告的路径 ID。

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

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ DSM \_ 路径**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_mpio_dsm_path) 数据结构。 没有与此 WMI 类相关联的方法。

 

