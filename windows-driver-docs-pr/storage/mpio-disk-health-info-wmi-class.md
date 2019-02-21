---
title: MPIO\_磁盘\_运行状况\_信息 WMI 类
description: MPIO\_磁盘\_运行状况\_信息 WMI 类
ms.assetid: 5a3ca8be-8940-4ba4-9206-75d0c7c90d53
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d85cf76339f5f411a767adcfaa55a3c7d5fe1d20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525486"
---
# <a name="mpiodiskhealthinfo-wmi-class"></a>MPIO\_磁盘\_运行状况\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_磁盘\_运行状况\_它所管理的所有 MPIO 磁盘以报告运行状况统计信息的信息 WMI 类。

```cpp
class MPIO_DISK_HEALTH_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    [WmiDataId(1),
     read,
     Description("Number of Pseudo-LUN Health Packets.") : amended
    ] uint32 NumberDiskPackets;

    [WmiDataId(2),
     read,
     Description("Reserved for future use.") : amended
    ] uint32 Reserved;

    [WmiDataId(3),
     read,
     Description("MPIO Pseudo-LUN Health Info Array.") : amended,
     WmiSizeIs("NumberDiskPackets")
    ] MPIO_DISK_HEALTH_CLASS DiskHealthPackets[];
};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_磁盘\_运行状况\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff562359)数据结构。 没有与此 WMI 类相关联的方法。

 

 





