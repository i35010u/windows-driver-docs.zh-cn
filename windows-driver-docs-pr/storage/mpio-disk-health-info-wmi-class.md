---
title: MPIO\_磁盘\_运行状况\_信息 WMI 类
description: MPIO\_磁盘\_运行状况\_信息 WMI 类
ms.assetid: 5a3ca8be-8940-4ba4-9206-75d0c7c90d53
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26f557913e60f271c03c4dd4ee10a2ee52c05abd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386166"
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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_磁盘\_运行状况\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_disk_health_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





