---
title: DSM\_参数 WMI 类
description: DSM\_参数 WMI 类
ms.assetid: c946f8cb-327c-4d5a-a133-0051a405fcad
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f3fc0f478f369302520f5b861b3ad19d24d12ea7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380668"
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

此类定义编译时通过 WMI 工具套件，它会生成[ **DSM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff552713)数据结构。 没有与此 WMI 类相关联的方法。

 

 





