---
title: MPIO\_已注册\_DSM WMI 类
description: MPIO\_已注册\_DSM WMI 类
ms.assetid: 3be335bd-e5d8-4611-9ccf-bd7fb0457b61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dc5270747e93080250298617e67fe566043065d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386146"
---
# <a name="mpioregistereddsm-wmi-class"></a>MPIO\_已注册\_DSM WMI 类


WMI 客户端使用 MPIO\_已注册\_DSM WMI 类来查询系统中配置的所有 DSMs。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_已注册\_DSM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_registered_dsm)数据结构。 没有与此 WMI 类相关联的方法。

 

 





