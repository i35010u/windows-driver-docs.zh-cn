---
title: MPIO \_ DEVINSTANCE \_ HEALTH \_ 信息 WMI 类
description: MPIO \_ DEVINSTANCE \_ HEALTH \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8c40e16ed8f4aab0d6e35ea78c4854089fdb9a74
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835031"
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

 

