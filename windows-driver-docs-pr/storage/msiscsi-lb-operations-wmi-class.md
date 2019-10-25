---
title: MSiSCSI\_LB\_操作 WMI 类
description: MSiSCSI\_LB\_操作 WMI 类
ms.assetid: 75c93040-52bf-4e9c-a503-a87f382ee1c9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba6b6e620b2e18364132011593e40c50d8cd25d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845349"
---
# <a name="msiscsi_lb_operations-wmi-class"></a>MSiSCSI\_LB\_操作 WMI 类


MSiSCSI\_LB\_操作 WMI 类包含用于设置和检索负载平衡策略的方法。 此类在管理 mof 中定义为：

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

当 WMI 工具套件编译上述类定义时，它会生成一个[MSiSCSI\_LB\_操作](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)数据结构。

 

 





