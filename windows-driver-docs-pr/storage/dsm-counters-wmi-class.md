---
title: DSM \_ 计数器 WMI 类
description: DSM \_ 计数器 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b104f9260e93301ea9dc2103cd1a6beb580277a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804667"
---
# <a name="dsm_counters-wmi-class"></a>DSM \_ 计数器 WMI 类


MPIO 驱动程序使用 DSM \_ 计数器 WMI 类标识与 DSM 关联的所有计时器值。

```cpp
class DSM_COUNTERS
{
    //
    // Flag indicating if automatic path verification must be performed every
    // N seconds (where N depends on the value set in PathVerificationPeriod).
    // Type is boolean and must be filled with either 0 (disbale) or 1 (enable).
    //
    [WmiDataId(1)] uint32 PathVerifyEnabled;

    //
    // This timer is specified in seconds. It controls the periodicity
    // for path verification.
    //
    [WmiDataId(2)] uint32 PathVerificationPeriod;

    //
    // This timer is specified in seconds. It controls the amount of time
    // that the pseudo-LUN will continue to be in memory, even after
    // loosing all its paths.
    //
    [WmiDataId(3)] uint32 PDORemovePeriod;

    //
    // The number of times a failed I/O will be retried if DsmInterpretError
    // requests a retry.
    //
    [WmiDataId(4)] uint32 RetryCount;

    //
    // This value is specified in seconds. It controls the interval of time
    // after which a failed request is retried (after the DSM has decided so).
    //
    [WmiDataId(5)] uint32 RetryInterval;

    //
    // Reserved for future use.
    //
    [WmiDataId(6)] uint32 Reserved32;
    [WmiDataId(7)] uint64 Reserved64;

};
```

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ 计数器**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_counters) 数据结构。 没有与此 WMI 类相关联的方法。

 

