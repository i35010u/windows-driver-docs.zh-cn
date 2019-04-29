---
title: MPIO\_磁盘\_信息 WMI 类
description: MPIO\_磁盘\_信息 WMI 类
ms.assetid: 75c66c84-d815-43a5-a70d-1952bf0e8d44
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 29157213afa02c12e366f20850c33714e0e24be1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391409"
---
# <a name="mpiodiskinfo-wmi-class"></a>MPIO\_磁盘\_信息 WMI 类


WMI 客户端使用 MPIO\_磁盘\_在系统中配置 MPIO，以便它收集有关每个 MPIO 的信息的磁盘的查询的信息的 WMI 类。

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

此类定义时编译的 WMI 工具套件，生成[ **MPIO\_磁盘\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff562367)数据结构。 没有与此 WMI 类相关联的方法。

 

 





