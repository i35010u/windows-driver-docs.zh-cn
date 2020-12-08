---
title: MSiSCSI \_ QUERYLBPOLICY WMI 类
description: MSiSCSI \_ QUERYLBPOLICY WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4eba42e4e239838ba5cef11eb4f41ecdd44fa453
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821203"
---
# <a name="msiscsi_querylbpolicy-wmi-class"></a>MSiSCSI \_ QUERYLBPOLICY WMI 类


MSiSCSI \_ QUERYLBPOLICY WMI 类包含有关负载平衡策略的信息。 此类在 *管理 mof* 中定义为：

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

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ QueryLBPolicy**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_querylbpolicy) 数据结构。

 

