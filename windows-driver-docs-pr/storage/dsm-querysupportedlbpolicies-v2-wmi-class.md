---
title: DSM\_QuerySupportedLBPolicies\_V2 WMI 类
description: DSM\_QuerySupportedLBPolicies\_V2 WMI 类
ms.assetid: d60cf06d-595b-425d-bf22-f0986267ba09
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d05015071060fd7dc3c872c44c723c0600504531
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368224"
---
# <a name="dsmquerysupportedlbpoliciesv2-wmi-class"></a>DSM\_QuerySupportedLBPolicies\_V2 WMI 类


MPIO 发布 DSM\_QuerySupportedLBPolicies\_V2 WMI 类但需要进行注册，GUID 和处理其实现的 DSM。 WMI 客户端使用 DSM\_QuerySupportedLBPolicies\_V2 WMI 类，查询 DSM 支持的所有负载平衡策略。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_QuerySupportedLBPolicies\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_dsm_querysupportedlbpolicies_v2)数据结构。 没有与此 WMI 类相关联的方法。

 

 





