---
title: MSiSCSI\_QueryLBPolicy WMI 类
description: MSiSCSI\_QueryLBPolicy WMI 类
ms.assetid: 1d80f525-491a-4c81-8827-7c5c13107a54
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 64b9d20857e4c4b195a25fa2cea553bfbd185315
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565237"
---
# <a name="msiscsiquerylbpolicy-wmi-class"></a>MSiSCSI\_QueryLBPolicy WMI 类


MSiSCSI\_QueryLBPolicy WMI 类包含有关负载平衡策略的信息。 此类定义，如下所示在*Mgmt.mof。*

```cpp
class MSiSCSI_QueryLBPolicy 
{
    [key]
    string InstanceName;

    boolean Active;

    [WmiDataId(1),
     DisplayName("Adapter Id") : amended,
     DisplayInHex,
     Description("Id that is globally unique to each instance of each adapter. Using the address of the Adapter Extension is a good idea.") : amended
    ]
    uint64 UniqueAdapterId;

    [WmiDataId(2),
     read,
     DisplayName("Reserved field") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     DisplayName("Count of Elements in LoadBalancePolicies array") : amended,
     cpp_quote("\n    // Number of elements in LoadBalancePolicies array\n"),
     Description("Number of elements in LoadBalancePolicies array") : amended
    ] uint32 SessionCount;

    [WmiDataId(4),
     DisplayName("Load Balance Policy for each session") : amended,
     description("Load Balance Policy that is currently being used by iSCSI Initiator - one element for each session on the adapter") : amended,
     WmiSizeIs("SessionCount")
    ]
    ISCSI_Supported_LB_Policies LoadBalancePolicies[];
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_QueryLBPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff563107)数据结构。

 

 





