---
title: DSM \_ QueryLBPolicy \_ V2 WMI 类
description: DSM \_ QueryLBPolicy \_ V2 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ed3c6d27e2aa535460102c7c3149f347d02e5fb6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835329"
---
# <a name="dsm_querylbpolicy_v2-wmi-class"></a>DSM \_ QueryLBPolicy \_ V2 WMI 类


MPIO 发布 DSM \_ QUERYLBPolicy \_ V2 WMI 类，但要求 DSM 注册 GUID 并处理其实现。 WMI 客户端使用 DSM \_ QUERYLBPolicy \_ V2 WMI 类来查询为 MPIO 磁盘设置的负载平衡策略。

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

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ QueryLBPolicy \_ V2**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querylbpolicy_v2) 数据结构。 没有与此 WMI 类相关联的方法。

 

