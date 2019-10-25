---
title: MPIO\_DEVINSTANCE\_HEALTH\_信息 WMI 类
description: MPIO\_DEVINSTANCE\_HEALTH\_信息 WMI 类
ms.assetid: 4d47b41b-eac6-4f8b-801b-76eec8158074
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b1db90c4297cf84541920141eebd7fba158c4c68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844552"
---
# <a name="mpio_devinstance_health_info-wmi-class"></a>MPIO\_DEVINSTANCE\_HEALTH\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_DEVINSTANCE\_HEALTH\_信息 WMI 类通过使用基础不同路径来报告 MPIO 磁盘的运行状况统计信息。

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

当 WMI 工具套件编译此类定义时，它将生成[**MPIO\_DEVINSTANCE\_HEALTH\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_mpio_devinstance_health_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





