---
title: MPIO\_已注册\_DSM WMI 类
description: MPIO\_已注册\_DSM WMI 类
ms.assetid: 3be335bd-e5d8-4611-9ccf-bd7fb0457b61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2a0bc7e71000eba08061c133e8062e9e902ba080
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554344"
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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_已注册\_DSM** ](https://msdn.microsoft.com/library/windows/hardware/ff562449)数据结构。 没有与此 WMI 类相关联的方法。

 

 





