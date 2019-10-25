---
title: MPIO\_DEVINSTANCE\_HEALTH\_类 WMI 类
description: MPIO\_DEVINSTANCE\_HEALTH\_类 WMI 类
ms.assetid: d2c77461-d89c-4c1b-86dc-3373de0f11e4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2716c40abf0f9c2e5ed7f3839b997135734549cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844542"
---
# <a name="mpio_devinstance_health_class-wmi-class"></a>MPIO\_DEVINSTANCE\_HEALTH\_类 WMI 类


MPIO 驱动程序使用 MPIO\_DEVINSTANCE\_HEALTH\_类 WMI 类，通过特定路径报告设备的运行状况统计信息。

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

当 WMI 工具套件编译此类定义时，它将生成[**MPIO\_DEVINSTANCE\_HEALTH\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_mpio_devinstance_health_class)数据结构。 没有与此 WMI 类相关联的方法。

 

 





