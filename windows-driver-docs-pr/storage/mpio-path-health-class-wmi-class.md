---
title: MPIO \_ 路径 \_ 运行状况 \_ 类 WMI 类
description: MPIO \_ 路径 \_ 运行状况 \_ 类 WMI 类
ms.assetid: fcbc86a4-9035-489e-a406-9901c5af0a32
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0d60a3091866628137770cdce1244a7211c9345a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187531"
---
# <a name="mpio_path_health_class-wmi-class"></a>MPIO \_ 路径 \_ 运行状况 \_ 类 WMI 类


WMI 客户端使用 MPIO \_ 路径 \_ 运行状况 \_ 类 WMI 类来查询 mpio 子系统，以便为与 mpio 磁盘关联的特定路径收集运行状况统计信息。

```cpp
class MPIO_PATH_HEALTH_CLASS
{
    //
    // Identifier representing the path.
    //
    [WmiDataId(1),     read,     Description("Path identifier.") : amended    ] uint64 PathId;

    //
    // Number of read requests serviced by this path.
    //
    [WmiDataId(2),     read,     Description("Number of read requests serviced by this path.") : amended
    ] uint64 NumberReads;

    //
    // Number of writes serviced by this path.
    //
    [WmiDataId(3),
     read,
     Description("Number of writes serviced by this path.") : amended
    ] uint64 NumberWrites;

    //
    // Cumulative number of bytes read by requests serviced by this path.
    //
    [WmiDataId(4),
     read,
     Description("Cumulative number of bytes read by requests serviced by this path.") : amended
    ] uint64 NumberBytesRead;

    //
    // Cumulative number of bytes written by requests serviced by this path.
    //
    [WmiDataId(5),
     read,
     Description("Cumulative number of bytes written by requests serviced by this path.") : amended
    ] uint64 NumberBytesWritten;

    //
    // Number of requests retried using this path.
    //
    [WmiDataId(6),
     read,
     Description("Number of requests retried using this path.") : amended
    ] uint64 NumberRetries;

    //
    // Number of requests serviced by this path that failed.
    //
    [WmiDataId(7),
     read,
     Description("Number of requests serviced by this path that failed.") : amended
    ] uint64 NumberIoErrors;

    //
    // System time at which this health packet was created for this path.
    //
    [WmiDataId(8),
     read,
     Description("System time at which this health packet was created for this path.") : amended
    ] uint64 CreateTime;

    //
    // System time at which this path went offline/failed.
    //
    [WmiDataId(9),
     read,
     Description("System time at which this path went offline/failed.") : amended
    ] uint64 FailTime;

    //
    // Flag that indicates if the path is offline/failed.
    //
    [WmiDataId(10),
     read,
     Description("Flag that indicates if the path is offline/failed") : amended
    ] boolean PathOffline;

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
    // Number of requests sent down this path that are in flight.
    //
    [WmiDataId(15),
     read,
     Description("Number of requests sent down this path that are currently in flight.") : amended
    ] uint8 OutstandingRequests;

    //
    // Pad for data alignment.
    //
    [WmiDataId(16),
     read
    ] uint8 Pad[2];
};
```

由 WMI 工具套件编译时，此类定义生成 [**MPIO \_ 路径 \_ 运行状况 \_ 类**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_path_health_class) 数据结构。 没有与此 WMI 类相关联的方法。

 

