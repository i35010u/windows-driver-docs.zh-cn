---
title: DSM\_参数 WMI 类
description: DSM\_参数 WMI 类
ms.assetid: c946f8cb-327c-4d5a-a133-0051a405fcad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 418fd4df986cbde09e9f20b85434c1d09553911b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368243"
---
# <a name="dsmparameters-wmi-class"></a>DSM\_参数 WMI 类


MPIO 驱动程序用户 DSM\_参数 WMI 类，以标识 DSM 及其所有关联的计时器值。

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

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_dsm_parameters)数据结构。 没有与此 WMI 类相关联的方法。

 

 





