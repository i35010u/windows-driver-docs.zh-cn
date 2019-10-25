---
title: MPIO\_磁盘\_运行状况\_信息 WMI 类
description: MPIO\_磁盘\_运行状况\_信息 WMI 类
ms.assetid: 5a3ca8be-8940-4ba4-9206-75d0c7c90d53
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 884804b867f4800c6357ce76874ab2685266febd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844978"
---
# <a name="mpio_disk_health_info-wmi-class"></a>MPIO\_磁盘\_运行状况\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_磁盘\_HEALTH\_信息 WMI 类来报告它所管理的所有 MPIO 磁盘的运行状况统计信息。

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

当 WMI 工具套件编译此类定义时，它将生成[**MPIO\_磁盘\_运行状况\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_disk_health_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





