---
title: DSM\_QuerySupportedLBPolicies\_V2 WMI 类
description: DSM\_QuerySupportedLBPolicies\_V2 WMI 类
ms.assetid: d60cf06d-595b-425d-bf22-f0986267ba09
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7cb3467ecc565e42f1bb1d9703d88ffdb799e0fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843222"
---
# <a name="dsm_querysupportedlbpolicies_v2-wmi-class"></a>DSM\_QuerySupportedLBPolicies\_V2 WMI 类


MPIO 发布 DSM\_QuerySupportedLBPolicies\_V2 WMI 类，但要求 DSM 注册 GUID 并处理其实现。 WMI 客户端使用 DSM\_QuerySupportedLBPolicies\_V2 WMI 类来查询 DSM 支持的所有负载平衡策略。

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

当 WMI 工具套件编译此类定义时，它将生成[**DSM\_QuerySupportedLBPolicies\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querysupportedlbpolicies_v2)数据结构。 没有与此 WMI 类相关联的方法。

 

 





