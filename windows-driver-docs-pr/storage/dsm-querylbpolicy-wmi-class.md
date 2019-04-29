---
title: DSM\_QueryLBPolicy WMI 类
description: DSM\_QueryLBPolicy WMI 类
ms.assetid: b7fc0d38-feaa-46c5-bcde-fcd6c71b329b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ff547c38ecbc133003bab2f83cee0d4e87be108e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380665"
---
# <a name="dsmquerylbpolicy-wmi-class"></a>DSM\_QueryLBPolicy WMI 类


MPIO 发布 DSM\_QUERYLBPolicy\_V2 WMI 类但需要进行注册，GUID 和处理其实现的 DSM。 WMI 客户端使用 DSM\_QUERYLBPolicy\_V2 WMI 类，查询的负载平衡策略设置为 MPIO 的磁盘。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_QueryLBPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff552719)数据结构。 没有与此 WMI 类相关联的方法。

 

 





