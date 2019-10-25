---
title: MPIO\_路径\_运行状况\_信息 WMI 类
description: MPIO\_路径\_运行状况\_信息 WMI 类
ms.assetid: 26c329d0-0d9c-4d24-bbe4-ebb7d7b36a89
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d2d8939b5c88914de4c8d8da497cabb999f5b267
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844962"
---
# <a name="mpio_path_health_info-wmi-class"></a>MPIO\_路径\_运行状况\_信息 WMI 类


WMI 客户端使用 MPIO\_路径\_运行状况\_信息 WMI 类来查询 MPIO，以便它收集 MPIO 管理的所有路径的统计信息。

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

当通过 WMI 工具编译类定义时，suiteit 会生成[**MPIO\_路径\_HEALTH\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_path_health_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





