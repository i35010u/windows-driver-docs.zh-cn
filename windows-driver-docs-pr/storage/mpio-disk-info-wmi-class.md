---
title: MPIO\_磁盘\_信息 WMI 类
description: MPIO\_磁盘\_信息 WMI 类
ms.assetid: 75c66c84-d815-43a5-a70d-1952bf0e8d44
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c35ab052a7b69d18e5cae68bbf5c86e7ab355011
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844976"
---
# <a name="mpio_disk_info-wmi-class"></a>MPIO\_磁盘\_信息 WMI 类


WMI 客户端使用 MPIO\_磁盘\_信息 WMI 类来查询 MPIO，以便收集有关系统中配置的每个 MPIO 磁盘的信息。

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

由 WMI 工具套件编译时，此类定义生成[**MPIO\_磁盘\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_disk_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





