---
title: DSM\_QuerySupportedLBPolicies WMI 类
description: DSM\_QuerySupportedLBPolicies WMI 类
ms.assetid: fab4d9e6-68fb-42f8-89e5-a5f5b2580964
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eb980544740617b6a55aa812faeba8c4e4fcb24a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380660"
---
# <a name="dsmquerysupportedlbpolicies-wmi-class"></a>DSM\_QuerySupportedLBPolicies WMI 类


MPIO 发布 DSM\_QuerySupportedLBPolicies\_V2 WMI 类但需要进行注册，GUID 和处理其实现的 DSM。 WMI 客户端使用 DSM\_QuerySupportedLBPolicies\_V2 WMI 类，查询 DSM 支持的所有负载平衡策略。

```cpp
class DSM_QuerySupportedLBPolicies
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
    DSM_Load_Balance_Policy Supported_LB_Policies[];
};
```

此类定义中编译的 WMI 工具套件，此类定义生成时[ **DSM\_QuerySupportedLBPolicies** ](https://msdn.microsoft.com/library/windows/hardware/ff552733)数据结构。 没有与此 WMI 类相关联的方法。

 

 





