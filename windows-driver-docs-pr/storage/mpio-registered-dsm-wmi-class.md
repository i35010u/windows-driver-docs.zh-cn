---
title: MPIO \_ 注册的 \_ DSM WMI 类
description: MPIO \_ 注册的 \_ DSM WMI 类
ms.assetid: 3be335bd-e5d8-4611-9ccf-bd7fb0457b61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f6ca792559bf0c2e43e135768b594058c2d3c64d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187533"
---
# <a name="mpio_registered_dsm-wmi-class"></a>MPIO \_ 注册的 \_ DSM WMI 类


WMI 客户端使用 MPIO \_ 注册的 \_ DSM WMI 类来查询在系统中配置的所有 dsm。

```cpp
class MPIO_REGISTERED_DSM
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // The Number of DSMs that have registered with MPIO.
    //
    [WmiDataId(1),
     read,
     Description("Number of registered DSMs.") : amended
    ] uint32 NumberDSMs;

    //
    // Variable-length array of DSM_PARAMETERS structures.
    // NOTE: Each entry will be ULONG aligned. App. writers
    // take note when iterating through the array.
    //
    [WmiDataId(2),
     read,
     Description("Counters information of registered DSMs.") : amended,
     WmiSizeIs("NumberDSMs")
    ] DSM_PARAMETERS DsmParameters[];
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO 注册的 \_ \_ DSM**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_registered_dsm) 数据结构。 没有与此 WMI 类相关联的方法。

 

