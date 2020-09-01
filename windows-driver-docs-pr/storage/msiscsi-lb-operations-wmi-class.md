---
title: MSiSCSI \_ LB \_ 操作 WMI 类
description: MSiSCSI \_ LB \_ 操作 WMI 类
ms.assetid: 75c93040-52bf-4e9c-a503-a87f382ee1c9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f8674616b86f6029ce3f96e6533637e8877e7c01
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188925"
---
# <a name="msiscsi_lb_operations-wmi-class"></a>MSiSCSI \_ LB \_ 操作 WMI 类


MSiSCSI \_ LB \_ 操作 WMI 类包含用于设置和检索负载平衡策略的方法。 此类在管理 mof 中定义为：

```cpp
class MSiSCSI_LB_Operations {

    [key, read]
    string InstanceName;

    [read] 
    boolean Active;

    //
    // Method to set load balance policy for the iSCSI Initiator
    //
    [WmiMethodId(10),
     Implemented,
     Description("Sets Load Balance Policy for the iSCSI Initiator") : amended,
     cpp_quote(
       "//\n"
       "// SetLoadBalancePolicy instructs the iSCSI Initiator what Load Balance\n"
       "// policy to use.\n"
       "//\n"
              )            
    ]
    void SetLoadBalancePolicy(
        [in,
         Description("New Load Balance policy to be set")
        ] ISCSI_Supported_LB_Policies LoadBalancePolicies,

        [out,
         Description("Status of the operation")
        ] uint32 Status
    );
};
```

当 WMI 工具套件编译上述类定义时，它会生成一个 [MSiSCSI \_ LB \_ 操作](/windows-hardware/drivers/ddi/index) 数据结构。

 

