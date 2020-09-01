---
title: DSM \_ QUERYLBPOLICY WMI 类
description: DSM \_ QUERYLBPOLICY WMI 类
ms.assetid: b7fc0d38-feaa-46c5-bcde-fcd6c71b329b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 30a3d793a3b4eb83f30602e6d269575dc0c50f3f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190223"
---
# <a name="dsm_querylbpolicy-wmi-class"></a>DSM \_ QUERYLBPOLICY WMI 类


MPIO 发布 DSM \_ QUERYLBPolicy \_ V2 WMI 类，但要求 DSM 注册 GUID 并处理其实现。 WMI 客户端使用 DSM \_ QUERYLBPolicy \_ V2 WMI 类查询为 MPIO 磁盘设置的负载平衡策略。

```cpp
class DSM_QueryLBPolicy
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    [WmiDataId(1),
     DisplayName("Load Balance Policy") : amended,
     Description("Load Balance Policy that is currently being used by DSM") : amended
    ]
    DSM_Load_Balance_Policy LoadBalancePolicy;
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ QueryLBPolicy**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querylbpolicy) 数据结构。 没有与此 WMI 类相关联的方法。

 

