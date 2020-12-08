---
title: MPIO \_ 注册的 \_ DSM WMI 类
description: MPIO \_ 注册的 \_ DSM WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c430304d7312b5acf344fcc4af4a5d1ddf178188
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835009"
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

 

