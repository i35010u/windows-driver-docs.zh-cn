---
title: '\_DSM WMI 类注册了 MPIO\_'
description: '\_DSM WMI 类注册了 MPIO\_'
ms.assetid: 3be335bd-e5d8-4611-9ccf-bd7fb0457b61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cb832ee0201ae52fc9207244098a92bc3d833037
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843568"
---
# <a name="mpio_registered_dsm-wmi-class"></a>\_DSM WMI 类注册了 MPIO\_


WMI 客户端使用\_DSM WMI 类注册的 MPIO\_来查询在系统中配置的所有 Dsm。

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

当 WMI 工具套件编译此类定义时，它将生成[**MPIO\_注册\_DSM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_registered_dsm)数据结构。 没有与此 WMI 类相关联的方法。

 

 





