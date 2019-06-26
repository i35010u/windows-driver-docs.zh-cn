---
title: MPIO\_DEVINSTANCE\_运行状况\_信息 WMI 类
description: MPIO\_DEVINSTANCE\_运行状况\_信息 WMI 类
ms.assetid: 4d47b41b-eac6-4f8b-801b-76eec8158074
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b8f042175e979fdb8bc60ecacc68b426397928a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386170"
---
# <a name="mpiodevinstancehealthinfo-wmi-class"></a>MPIO\_DEVINSTANCE\_运行状况\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_DEVINSTANCE\_运行状况\_信息 WMI 类传递给报表运行状况统计信息通过使用基础的不同路径的 MPIO 磁盘。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_DEVINSTANCE\_运行状况\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_mpio_devinstance_health_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





