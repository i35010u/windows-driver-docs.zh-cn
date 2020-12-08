---
title: MPIO \_ 磁盘 \_ 信息 WMI 类
description: MPIO \_ 磁盘 \_ 信息 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6fb7579e745abe658c1eee69b9a47f08034db011
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811571"
---
# <a name="mpio_disk_info-wmi-class"></a>MPIO \_ 磁盘 \_ 信息 WMI 类


WMI 客户端使用 MPIO \_ 磁盘 \_ 信息 WMI 类来查询 MPIO，以便收集有关系统中配置的每个 MPIO 磁盘的信息。

```cpp
class MPIO_DISK_INFO
{
    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // The Number of multi-path disk pdos that have been
    // created.
    //
    [WmiDataId(1),
     read,
     Description("Number of Multi-Path Drives.") : amended
    ] uint32 NumberDrives;

    //
    // Variable-length array of DRIVE_INFO structures.
    // NOTE: Each entry will be ULONG aligned. App. writers
    // take note when iterating through the array.
    //
    [WmiDataId(2),
     read,
     Description("Multi-Path Drive Info Array.") : amended,
     WmiSizeIs("NumberDrives")
    ] MPIO_DRIVE_INFO DriveInfo[];
};
```

由 WMI 工具套件编译时，此类定义生成 [**MPIO \_ 磁盘 \_ 信息**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_disk_info) 数据结构。 没有与此 WMI 类相关联的方法。

 

