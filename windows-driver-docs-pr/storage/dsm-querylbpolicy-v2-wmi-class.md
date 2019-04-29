---
title: DSM\_QueryLBPolicy\_V2 WMI 类
description: DSM\_QueryLBPolicy\_V2 WMI 类
ms.assetid: 748db832-9ddb-4ca0-a229-9f5d95f5c24b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 05411785eae164ada0dec55aa3fbbd5116b97052
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380666"
---
# <a name="dsmquerylbpolicyv2-wmi-class"></a>DSM\_QueryLBPolicy\_V2 WMI 类


MPIO 发布 DSM\_QUERYLBPolicy\_V2 WMI 类但需要进行注册，GUID 和处理其实现的 DSM。 WMI 客户端使用 DSM\_QUERYLBPolicy\_V2 WMI 类，查询的 MPIO 磁盘设置负载平衡策略。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_QueryLBPolicy\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff552724)数据结构。 没有与此 WMI 类相关联的方法。

 

 





