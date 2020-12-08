---
title: MPIO \_ 路径 \_ 运行状况 \_ 信息 WMI 类
description: MPIO \_ 路径 \_ 运行状况 \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1010fa8bad71f7fa6ee10b3e0a723fcc744b5145
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835011"
---
# <a name="mpio_path_health_info-wmi-class"></a>MPIO \_ 路径 \_ 运行状况 \_ 信息 WMI 类


WMI 客户端使用 MPIO \_ 路径 \_ 运行状况 \_ 信息 WMI 类来查询 mpio，以便它收集 mpio 管理的所有路径的统计信息。

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

当使用 WMI 工具编译类定义时，suiteit 将生成 [**MPIO \_ 路径 \_ 运行状况 \_ 信息**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_path_health_info) 数据结构。 没有与此 WMI 类相关联的方法。

 

