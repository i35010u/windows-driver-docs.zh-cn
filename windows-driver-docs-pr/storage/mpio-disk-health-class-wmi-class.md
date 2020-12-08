---
title: MPIO \_ 磁盘 \_ 运行状况 \_ 类 WMI 类
description: MPIO \_ 磁盘 \_ 运行状况 \_ 类 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d6218d6949df96a53a868fafb0f6ab18e3181277
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811573"
---
# <a name="mpio_disk_health_class-wmi-class"></a>MPIO \_ 磁盘 \_ 运行状况 \_ 类 WMI 类


MPIO 驱动程序使用 MPIO \_ 磁盘 \_ 运行状况 \_ 类 WMI 类来报告 MPIO 磁盘的运行状况统计信息。

```cpp
class MPIO_DISK_HEALTH_CLASS
{
    //
    // The MPIODisk(N).
    //
    [WmiDataId(1), MaxLen(63)] string Name;

    //
    // Number of read requests sent to this device.
    //
    [WmiDataId(2),
     read,
     Description("Number of read requests sent to this device.") : amended
    ] uint64 NumberReads;

    //
    // Number of write requests sent to this device.
    //
    [WmiDataId(3),
     read,
     Description("Number of write requests sent to this device.") : amended
    ] uint64 NumberWrites;

    //
    // Cumulative number of bytes read by requests sent to this device.
    //
    [WmiDataId(4),
     read,
     Description("Cumulative number of bytes read by requests sent to this device.") : amended
    ] uint64 NumberBytesRead;

    //
    // Cumulative number of bytes written by requests sent to this device.
    //
    [WmiDataId(5),
     read,
     Description("Cumulative number of bytes written by requests sent to this device.") : amended
    ] uint64 NumberBytesWritten;

    //
    // Number of requests sent to this device that were retried.
    //
    [WmiDataId(6),
     read,
     Description("Number of requests sent to this device that were retried.") : amended
    ] uint64 NumberRetries;

    //
    // Number of requests sent to this device that failed.
    //
    [WmiDataId(7),
     read,
     Description("Number of requests sent to this device that failed.") : amended
    ] uint64 NumberIoErrors;

    //
    // System time at which this health packet was created for this device.
    //
    [WmiDataId(8),
     read,
     Description("System time at which this health packet was created for this device.") : amended
    ] uint64 CreateTime;

    //
    // Number of path failures experienced by this device.
    //
    [WmiDataId(9),
     read,
     Description("Number of path failures experienced by this device.") : amended
    ] uint64 PathFailures;

    //
    // System time at which this device went offline/failed.
    //
    [WmiDataId(10),
     read,
     Description("System time at which this device went offline/failed.") : amended
    ] uint64 FailTime;

    //
    // Flag that indicates if the device is offline/failed.
    //
    [WmiDataId(11),
     read,
     Description("Flag that indicates if the device is offline/failed.") : amended
    ] boolean DeviceOffline;

    //
    // Count of the number of times that the NumberReads field wrapped.
    //
    [WmiDataId(12),
     read,
     Description("Count of the number of times that the NumberReads field wrapped.") : amended
    ] uint8 NumberReadsWrap;

    //
    // Count of the number of times that the NumberWrites field wrapped.
    //
    [WmiDataId(13),
     read,
     Description("Count of the number of times that the NumberWrites field wrapped.") : amended
    ] uint8 NumberWritesWrap;

    //
    // Count of the number of times that the NumberBytesRead field wrapped.
    //
    [WmiDataId(14),
     read,
     Description("Count of the number of times that the NumberBytesRead field wrapped.") : amended
    ] uint8 NumberBytesReadWrap;

    //
    // Count of the number of times that the NumberBytesWritten field wrapped.
    //
    [WmiDataId(15),
     read,
     Description("Count of the number of times that the NumberBytesWritten field wrapped.") : amended
    ] uint8 NumberBytesWrittenWrap;

    //
    // Pad for data alignment.
    //
    [WmiDataId(16),
     read
    ] uint8 Pad[3];
};
```

当 WMI 工具套件编译类定义时，它将生成 [**MPIO \_ 磁盘 \_ 运行状况 \_ 类**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_disk_health_class) 数据结构。 没有与此 WMI 类相关联的方法。

 

