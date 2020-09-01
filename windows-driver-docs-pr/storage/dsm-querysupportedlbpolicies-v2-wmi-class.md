---
title: DSM \_ QuerySupportedLBPolicies \_ V2 WMI 类
description: DSM \_ QuerySupportedLBPolicies \_ V2 WMI 类
ms.assetid: d60cf06d-595b-425d-bf22-f0986267ba09
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d508a174765a49a1200e11274b8298235015290
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192671"
---
# <a name="dsm_querysupportedlbpolicies_v2-wmi-class"></a>DSM \_ QuerySupportedLBPolicies \_ V2 WMI 类


MPIO 发布 DSM \_ QuerySupportedLBPolicies \_ V2 WMI 类，但要求 DSM 注册 GUID 并处理其实现。 WMI 客户端使用 DSM \_ QuerySupportedLBPolicies \_ V2 WMI 类来查询 DSM 支持的所有负载平衡策略。

```cpp
class DSM_QuerySupportedLBPolicies_V2
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    [WmiDataId(1),
     Description("Number of supported Load Balance policies") : amended
    ]
    uint32 SupportedLBPoliciesCount;

    [WmiDataId(2),
     Description("Reserved") : amended
    ]
    uint32 Reserved;

    [WmiDataId(3),
     WmiSizeIs("SupportedLBPoliciesCount"),
     Description("Supported Load Balance Policies array") : amended
    ]
    DSM_Load_Balance_Policy_V2 Supported_LB_Policies[];
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ QuerySupportedLBPolicies \_ V2**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querysupportedlbpolicies_v2) 数据结构。 没有与此 WMI 类相关联的方法。

 

