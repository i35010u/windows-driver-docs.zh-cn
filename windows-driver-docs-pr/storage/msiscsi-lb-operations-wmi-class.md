---
title: MSiSCSI \_ LB \_ 操作 WMI 类
description: MSiSCSI \_ LB \_ 操作 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 590bb2838053d431fb2288bf4e29eea0ea93ecf4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804425"
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

 

