---
title: DSM\_参数 WMI 类
description: DSM\_参数 WMI 类
ms.assetid: c946f8cb-327c-4d5a-a133-0051a405fcad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6d2a295c01a7f5b215e34d76a91f0dd830ee2c79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844572"
---
# <a name="dsm_parameters-wmi-class"></a>DSM\_参数 WMI 类


MPIO 驱动程序用户使用 DSM\_参数 WMI 类标识 DSM 及其所有关联的计时器值。

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

当 WMI 工具套件编译此类定义时，它将生成[**DSM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_dsm_parameters)数据结构。 没有与此 WMI 类相关联的方法。

 

 





