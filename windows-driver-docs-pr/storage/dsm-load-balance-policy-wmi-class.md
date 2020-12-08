---
title: DSM \_ 负载 \_ 均衡 \_ 策略 WMI 类
description: DSM \_ 负载 \_ 均衡 \_ 策略 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 86c7844a94af41418c1a6c451d492b9ed6b2e0ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811743"
---
# <a name="dsm_load_balance_policy-wmi-class"></a>DSM \_ 负载 \_ 均衡 \_ 策略 WMI 类


MPIO 发布 DSM \_ 负载 \_ 平衡 \_ 策略 \_ V2 WMI 类，但要求 DSM 注册 GUID 并处理其实现。 MPIO 驱动程序使用 DSM \_ 负载 \_ 平衡 \_ 策略 \_ V2 WMI 类来确定应用于 MPIO 磁盘的负载平衡策略。

```cpp
class DSM_Load_Balance_Policy
{

    //
    // Version information for further changes.
    //
    [WmiDataId(1),
     read,
     Description("Version Number") : amended
    ]
    uint32 Version;

    //
    // Load Balance type.
    //
    [WmiDataId(2),
     Description("Load Balance Policy implemented by the DSM") : amended,
     Values{"Fail Over Only",
            "Round Robin",
            "Round Robin with Subset",
            "Dynamic Least Queue Depth",
            "Weighted Paths",
            "Least Blocks",
            "Vendor Specific"} : amended,

     DefineValues{"DSM_LB_FAILOVER",
                  "DSM_LB_ROUND_ROBIN",
                  "DSM_LB_ROUND_ROBIN_WITH_SUBSET",
                  "DSM_LB_DYN_LEAST_QUEUE_DEPTH",
                  "DSM_LB_WEIGHTED_PATHS",
                  "DSM_LB_LEAST_BLOCKS",
                  "DSM_LB_VENDOR_SPECIFIC"},
     ValueMap{"1", "2", "3", "4", "5", "6", "7"}
    ]
    uint32 LoadBalancePolicy;

    //
    // If load balance policy is DSM_LB_VENDOR_SPECIFIC then the following
    // properties are not used. The caller would need to provide data for
    // setting the vendor specific Load Balance policy.
    //

    //
    // Number of paths.
    //
    [WmiDataId(3),
     Description("Number of entries in DSM_Paths array") : amended
    ]
    uint32 DSMPathCount;

    [WmiDataId(4),
     Description("Reserved field") : amended
    ]
    uint32 Reserved;

    //
    // Paths' array.
    //
    [WmiDataId(5),
     WmiSizeIs("DSMPathCount"),
     Description("DSM_Paths array") : amended
    ]
    MPIO_DSM_Path DSM_Paths[];
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ 负载 \_ 平衡 \_ 策略**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_load_balance_policy) 数据结构。 没有与此 WMI 类相关联的方法。

 

