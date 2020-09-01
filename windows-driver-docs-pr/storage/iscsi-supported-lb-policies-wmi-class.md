---
title: 支持 ISCSI 的 \_ \_ LB \_ 策略 WMI 类
description: 支持 ISCSI 的 \_ \_ LB \_ 策略 WMI 类
ms.assetid: c11eebe8-519a-473d-9e9c-8a787333223e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ef37565fc3ddf289a07a4fd6af85dedc851a91d6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187829"
---
# <a name="iscsi_supported_lb_policies-wmi-class"></a>支持 ISCSI 的 \_ \_ LB \_ 策略 WMI 类


支持 ISCSI \_ 的 \_ LB \_ 策略 WMI 类包含有关支持多连接 ISCSI 会话的负载平衡策略的信息。 此类在*管理 mof*中定义为：

```cpp
class ISCSI_Supported_LB_Policies {

    [WmiDataId(1),
     description("Id that is unique to this session within this adapter. ") : amended
    ]
    uint64 UniqueSessionId;

    [WmiDataId(2),
     Description("Load Balance policy supported by the iSCSI Initiator") : amended,
     Values{"Fail Over Only",
            "Round Robin",
            "Round Robin with Subset",
            "Dynamic Least Queue Depth",
            "Weighted Paths",
            "Vendor Specific"} : amended,
     DefineValues{"MSiSCSI_LB_FAILOVER",
                  "MSiSCSI_LB_ROUND_ROBIN",
                  "MSiSCSI_LB_ROUND_ROBIN_WITH_SUBSET",
                  "MSiSCSI_LB_DYN_LEAST_QUEUE_DEPTH",
                  "MSiSCSI_LB_WEIGHTED_PATHS",
                  "MSiSCSI_LB_VENDOR_SPECIFIC"},
     ValueMap{"1", "2", "3", "4", "5", "6"}
    ] 
    uint32 LoadBalancePolicy;
 
    //
    // If load balance policy is MSiSCSI_LB_VENDOR_SPECIFIC then 
    // the following properties are not used. Instead the caller would 
    // need to provide data for setting the vendor specific
    // Load Balance policy.
    //
    [WmiDataId(3),
     Description("Number of entries in MSiSCSI_Paths array") : amended
    ]

    uint32 iSCSI_PathCount;

    [WmiDataId(4),
     WmiSizeIs("iSCSI_PathCount"),
     Description("Describes iSCSI Initiator Paths") : amended
    ]
    ISCSI_Path iSCSI_Paths[];
};
```

当 WMI 工具套件编译上述类定义时，它将生成 [**支持 ISCSI \_ 的 \_ LB \_ 策略**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_supported_lb_policies) 数据结构。

 

