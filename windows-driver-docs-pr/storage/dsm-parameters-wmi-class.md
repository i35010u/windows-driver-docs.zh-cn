---
title: DSM \_ 参数 WMI 类
description: DSM \_ 参数 WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b9b573066a1d8c5c74e92d5ec572aec6fe282051
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804661"
---
# <a name="dsm_parameters-wmi-class"></a>DSM \_ 参数 WMI 类


MPIO 驱动程序用户使用 DSM \_ 参数 WMI 类标识 dsm 及其所有关联的计时器值。

```cpp
class DSM_PARAMETERS
{
    //
    // Friendly name of the registered DSM.
    //
    [WmiDataId(1), MaxLen(63)] string DsmName;

    //
    // DSM-unique handle.
    //
    [WmiDataId(2)] uint64 DsmContext;

    //
    // Version Info
    //
    [WmiDataId(3)] DSM_VERSION DsmVersion;

    //
    // Counters Info
    //
    [WmiDataId(4)] DSM_COUNTERS DsmCounters;
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ 参数**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_parameters) 的数据结构。 没有与此 WMI 类相关联的方法。

 

