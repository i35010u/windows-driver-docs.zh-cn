---
title: MPIO \_ 计时器 \_ 计数器 WMI 类
description: MPIO \_ 计时器 \_ 计数器 WMI 类
ms.assetid: 386110f8-504c-4617-b8ae-557ea504d41d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fb51c05046166a240d313b4811de7a10226a9b47
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184209"
---
# <a name="mpio_timers_counters-wmi-class"></a>MPIO \_ 计时器 \_ 计数器 WMI 类


WMI 客户端使用 MPIO \_ 计时器 \_ 计数器 WMI 类来查询 MPIO 以查找所有全局计时器值。

```cpp
class MPIO_TIMERS_COUNTERS
{

    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Flag indicating if automatic path verification must be performed every
    // N seconds (where N depends on the value set in PathVerificationPeriod).
    // Type is boolean and must be filled with either 0 (disbale) or 1 (enable).
    //
    [WmiDataId(1),
     read, write,
     Description("Enable/Disable Auto Path-Verification.") : amended
    ] uint32 PathVerifyEnabled;

    //
    // This timer is specified in seconds. The default is 30 seconds
    // and its max allowed is MAXULONG. It controls the periodicity
    // for path verification.
    //
    [WmiDataId(2),
     read, write,
     Description("Path Verification Timer.") : amended
    ] uint32 PathVerificationPeriod;

    //
    // This timer is specified in seconds. The default is 20 seconds
    // and its max allowed is MAXULONG. It controls the amount of time
    // that the pseudo-LUN will continue to be in memory, even after
    // loosing all its paths.
    //
    [WmiDataId(3),
     read, write,
     Description("PDO Remove Timer.") : amended
    ] uint32 PDORemovePeriod;

    //
    // The number of times a failed I/O will be retried if DsmInterpretError
    // requests a retry. The default is set to 3.
    //
    [WmiDataId(4),
     read, write,
     Description("Request Retry Count (Max 500)") : amended
    ] uint32 RetryCount;

    //
    // This value is specified in seconds. The default is 1 second. It
    // controls the interval of time after which a failed request is
    // retried (after the DSM has decided so).
    //
    [WmiDataId(5),
     read, write,
     Description("Retry Interval (seconds) (Max MAXULONG)") : amended
    ] uint32 RetryInterval;

};
```

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ 计时器 \_ 计数器**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_timers_counters) 数据结构。 没有与此 WMI 类相关联的方法。

 

