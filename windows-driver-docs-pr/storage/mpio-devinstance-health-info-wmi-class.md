---
title: MPIO \_ DEVINSTANCE \_ HEALTH \_ 信息 WMI 类
description: MPIO \_ DEVINSTANCE \_ HEALTH \_ 信息 WMI 类
ms.assetid: 4d47b41b-eac6-4f8b-801b-76eec8158074
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0ec94e6fd8fcc0d75dd6d6de432645a900412dc5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190013"
---
# <a name="mpio_devinstance_health_info-wmi-class"></a>MPIO \_ DEVINSTANCE \_ HEALTH \_ 信息 WMI 类


MPIO 驱动程序使用 MPIO \_ DEVINSTANCE \_ HEALTH \_ INFO WMI 类通过使用基础不同路径来报告 MPIO 磁盘的运行状况统计信息。

```cpp
class MPIO_DEVINSTANCE_HEALTH_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    [WmiDataId(1),
     read,
     Description("Number of Health Packets.") : amended
    ] uint32 NumberDevInstancePackets;

    [WmiDataId(2),
     read,
     Description("Reserved for future use.") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     Description("Multi-Path Health Info Array.") : amended,
     WmiSizeIs("NumberDevInstancePackets")
    ] MPIO_DEVINSTANCE_HEALTH_CLASS DevInstanceHealthPackets[];
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ DEVINSTANCE \_ HEALTH \_ 信息**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_mpio_devinstance_health_info) 数据结构。 没有与此 WMI 类相关联的方法。

 

