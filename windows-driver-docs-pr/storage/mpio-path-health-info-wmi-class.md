---
title: MPIO\_路径\_运行状况\_信息 WMI 类
description: MPIO\_路径\_运行状况\_信息 WMI 类
ms.assetid: 26c329d0-0d9c-4d24-bbe4-ebb7d7b36a89
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cff2fa5b9c4476b8e7fe21b552503dcdd9545093
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561933"
---
# <a name="mpiopathhealthinfo-wmi-class"></a>MPIO\_路径\_运行状况\_信息 WMI 类


WMI 客户端使用 MPIO\_路径\_运行状况\_信息 WMI 类，以便它收集由 MPIO 管理的所有路径的统计信息查询 MPIO。

```cpp
class MPIO_PATH_HEALTH_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    [WmiDataId(1),
     read,
     Description("Number of Path Health Packets.") : amended
    ] uint32 NumberPathPackets;

    [WmiDataId(2),
     read,
     Description("Reserved for future use.") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     Description("MPIO Path Health Info Array.") : amended,
     WmiSizeIs("NumberPathPackets")
    ] MPIO_PATH_HEALTH_CLASS PathHealthPackets[];
};
```

类定义的 WMI 工具 suiteit 的编译时生成[ **MPIO\_路径\_运行状况\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff562431)数据结构。 没有与此 WMI 类相关联的方法。

 

 





