---
title: DSM\_计数器 WMI 类
description: DSM\_计数器 WMI 类
ms.assetid: 11ff77d7-5643-45ec-ac38-26ee70e6ea94
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b9f5a8bebf89044358d72d997a9932265de7ec7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368258"
---
# <a name="dsmcounters-wmi-class"></a>DSM\_计数器 WMI 类


MPIO 驱动程序使用 DSM\_计数器 WMI 类，以标识与 DSM 相关联的所有计时器值。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_计数器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_dsm_counters)数据结构。 没有与此 WMI 类相关联的方法。

 

 





