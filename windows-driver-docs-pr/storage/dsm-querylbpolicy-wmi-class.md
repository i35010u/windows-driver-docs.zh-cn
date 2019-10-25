---
title: DSM\_QueryLBPolicy WMI 类
description: DSM\_QueryLBPolicy WMI 类
ms.assetid: b7fc0d38-feaa-46c5-bcde-fcd6c71b329b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ecbe83523cf8215093c64f34e2081232e2e31dc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844568"
---
# <a name="dsm_querylbpolicy-wmi-class"></a>DSM\_QueryLBPolicy WMI 类


MPIO 发布 DSM\_QUERYLBPolicy\_V2 WMI 类，但要求 DSM 注册 GUID 并处理其实现。 WMI 客户端使用 DSM\_QUERYLBPolicy\_V2 WMI 类来查询为 MPIO 磁盘设置的负载平衡策略。

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

当 WMI 工具套件编译此类定义时，它将生成[**DSM\_QueryLBPolicy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_querylbpolicy)数据结构。 没有与此 WMI 类相关联的方法。

 

 





