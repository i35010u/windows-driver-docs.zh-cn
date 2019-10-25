---
title: DSM\_QueryLBPolicy\_V2 WMI 类
description: DSM\_QueryLBPolicy\_V2 WMI 类
ms.assetid: 748db832-9ddb-4ca0-a229-9f5d95f5c24b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d1e7c77784431af2c84d3e0b82e12cae3ea4273
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844570"
---
# <a name="dsm_querylbpolicy_v2-wmi-class"></a>DSM\_QueryLBPolicy\_V2 WMI 类


MPIO 发布 DSM\_QUERYLBPolicy\_V2 WMI 类，但要求 DSM 注册 GUID 并处理其实现。 WMI 客户端使用 DSM\_QUERYLBPolicy\_V2 WMI 类来查询为 MPIO 磁盘设置的负载平衡策略。

```cpp
class DSM_QueryLBPolicy_V2
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    [WmiDataId(1),
     DisplayName("Load Balance Policy") : amended,
     Description("Load Balance Policy that is currently being used by DSM") : amended
    ]
    DSM_Load_Balance_Policy_V2 LoadBalancePolicy;
};
```

当 WMI 工具套件编译此类定义时，它将生成[**DSM\_QueryLBPolicy\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querylbpolicy_v2)数据结构。 没有与此 WMI 类相关联的方法。

 

 





