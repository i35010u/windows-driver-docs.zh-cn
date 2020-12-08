---
title: MPIO \_ 磁盘 \_ 运行状况 \_ 信息 WMI 类
description: MPIO \_ 磁盘 \_ 运行状况 \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 91c9a83217970e162cb0bf9ab0785db4c4ccaaeb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835029"
---
# <a name="mpio_disk_health_info-wmi-class"></a>MPIO \_ 磁盘 \_ 运行状况 \_ 信息 WMI 类


MPIO 驱动程序使用 MPIO \_ 磁盘 \_ 健康 \_ 信息 WMI 类来报告它所管理的所有 MPIO 磁盘的运行状况统计信息。

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

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ 磁盘 \_ 健康 \_ 信息**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_disk_health_info) 数据结构。 没有与此 WMI 类相关联的方法。

 

