---
title: DSM \_ 参数 WMI 类
description: DSM \_ 参数 WMI 类
ms.assetid: c946f8cb-327c-4d5a-a133-0051a405fcad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1dfc19e05f64bd8c33893eb4f2f3946b99fe6654
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189443"
---
# <a name="dsm_parameters-wmi-class"></a>DSM \_ 参数 WMI 类


MPIO 驱动程序用户使用 DSM \_ 参数 WMI 类标识 dsm 及其所有关联的计时器值。

```cpp
class DSM_PARAMETERS
{
    //
    // Friendly name of the registered DSM.
    //
    [WmiDataId(1), MaxLen(63)] string DsmName;

    //
    // DSM-unique handle.
    //
    [WmiDataId(2)] uint64 DsmContext;

    //
    // Version Info
    //
    [WmiDataId(3)] DSM_VERSION DsmVersion;

    //
    // Counters Info
    //
    [WmiDataId(4)] DSM_COUNTERS DsmCounters;
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ 参数**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_parameters) 的数据结构。 没有与此 WMI 类相关联的方法。

 

