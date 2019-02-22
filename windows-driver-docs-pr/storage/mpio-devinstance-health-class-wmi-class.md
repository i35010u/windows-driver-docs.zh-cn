---
title: MPIO\_DEVINSTANCE\_运行状况\_类 WMI 类
description: MPIO\_DEVINSTANCE\_运行状况\_类 WMI 类
ms.assetid: d2c77461-d89c-4c1b-86dc-3373de0f11e4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6ea752a24f3a902cbf00bb93d3b093a53a0b13de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541494"
---
# <a name="mpiodevinstancehealthclass-wmi-class"></a>MPIO\_DEVINSTANCE\_运行状况\_类 WMI 类


MPIO 驱动程序使用 MPIO\_DEVINSTANCE\_运行状况\_类 WMI 类以报告运行状况统计信息的设备通过特定的路径。

```cpp
class MPIO_DEVINSTANCE_HEALTH_CLASS
{
    //
    // Path identifier through which this instance is exposed.
    //
    [WmiDataId(1),
     read,
     Description("Path identifier through which this device instance is exposed.") : amended
    ] uint64 PathId;

    //
    // Number of read requests serviced by this device through this instance.
    //
    [WmiDataId(2),
     read,
     Description("Number of read requests serviced by this device through this instance.") : amended
    ] uint64 NumberReads;

    //
    // Number of write requests serviced by this device through this instance.
    //
    [WmiDataId(3),
     read,
     Description("Number of write requests serviced by this device through this instance.") : amended
    ] uint64 NumberWrites;

    //
    // Cumulative number of bytes read on this device through this instance.
    //
    [WmiDataId(4),
     read,
     Description("Cumulative number of bytes read on this device through this instance.") : amended
    ] uint64 NumberBytesRead;

    //
    // Cumulative number of bytes written to this device through this instance.
    //
    [WmiDataId(5),
     read,
     Description("Cumulative number of bytes written to this device through this instance.") : amended
    ] uint64 NumberBytesWritten;

    //
    // Number of failed requests retried on this device using this instance.
    //
    [WmiDataId(6),
     read,
     Description("Number of failed requests retried on this device using this instance.") : amended
    ] uint64 NumberRetries;

    //
    // Number of requests to this device serviced by this instance that were failed back to the application.
    //
    [WmiDataId(7),
     read,
     Description("Number of requests to this device serviced by this instance that were failed back to the application.") : amended
    ] uint64 NumberIoErrors;

    //
    // System time when this device instance was exposed to the system.
    //
    [WmiDataId(8),
     read,
     Description("System time when this device instance was exposed to the system.") : amended
    ] uint64 CreateTime;

    //
    // System time when this device instance got removed from the system.
    //
    [WmiDataId(9),
     read,
     Description("System time when this device instance got removed from the system.") : amended
    ] uint64 FailTime;

    //
    // Flag that indicates if this device instance is removed from the system.
    //
    [WmiDataId(10),
     read,
     Description("Flag that indicates if this device instance is removed from the system.") : amended
    ] boolean DeviceOffline;

    //
    // Count of the number of times that the NumberReads field wrapped.
    //
    [WmiDataId(11),
     read,
     Description("Count of the number of times that the NumberReads field wrapped.") : amended
    ] uint8 NumberReadsWrap;

    //
    // Count of the number of times that the NumberWrites field wrapped.
    //
    [WmiDataId(12),
     read,
     Description("Count of the number of times that the NumberWrites field wrapped.") : amended
    ] uint8 NumberWritesWrap;

    //
    // Count of the number of times that the NumberBytesRead field wrapped.
    //
    [WmiDataId(13),
     read,
     Description("Count of the number of times that the NumberBytesRead field wrapped.") : amended
    ] uint8 NumberBytesReadWrap;

    //
    // Count of the number of times that the NumberBytesWritten field wrapped.
    //
    [WmiDataId(14),
     read,
     Description("Count of the number of times that the NumberBytesWritten field wrapped.") : amended
    ] uint8 NumberBytesWrittenWrap;

    //
    // Pad for data alignment.
    //
    [WmiDataId(15),
     read
    ] uint8 Pad[3];
};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_DEVINSTANCE\_运行状况\_类**](https://msdn.microsoft.com/library/windows/hardware/ff562337)数据结构。 没有与此 WMI 类相关联的方法。

 

 





