---
title: DSM\_QueryUniqueId WMI 类
description: DSM\_QueryUniqueId WMI 类
ms.assetid: 576e208d-972c-47ba-ab30-a05bf3d0943d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a747abe604f7c7030e82e5ff1ecd9a2a3fd2bff9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565334"
---
# <a name="dsmqueryuniqueid-wmi-class"></a>DSM\_QueryUniqueId WMI 类


MPIO 发布 DSM\_QueryUniqueId WMI 类但需要进行注册，GUID 和处理其实现的 DSM。 WMI 客户端使用 DSM\_QueryUniqueId WMI 类，查询路径的唯一标识符。

```cpp
class DSM_QueryUniqueId
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    //
    // This Identifier needs to be set by DSMs that want management applications
    // like VDS to be able to manage the devices controlled by the particular DSM.
    // This DsmUniqueId will be used in conjuction with the DsmPathId to construct
    // a path identitifer that is unique not just among all paths known to this DSM,
    // but also among all the DSMs present on the system.
    //
    [WmiDataId(1),
     DisplayName("DSM Unique Identifier") : amended,
     Description("DSM Unique Identifier to be used by a management application") : amended
    ]
    uint64 DsmUniqueId;
};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_QueryUniqueId** ](https://msdn.microsoft.com/library/windows/hardware/ff552742)数据结构。 没有与此 WMI 类相关联的方法。

 

 





