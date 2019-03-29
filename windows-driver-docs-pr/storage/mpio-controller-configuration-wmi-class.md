---
title: MPIO\_控制器\_配置 WMI 类
description: MPIO\_控制器\_配置 WMI 类
ms.assetid: c11429d6-b016-464e-a7b4-03b6cdc8ddb7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7bdec1e2404d168c8bce660c4808e271ed744d19
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350290"
---
# <a name="mpiocontrollerconfiguration-wmi-class"></a>MPIO\_控制器\_配置 WMI 类


WMI 客户端使用 MPIO\_控制器\_到有关连接到系统的存储控制器的信息的查询 MPIO 配置 WMI 类。

```cpp
class MPIO_CONTROLLER_CONFIGURATION
{

    [key, read]
     string InstanceName;
    [read] boolean Active;

    //
    // Number of controllers in the array.
    //
    [WmiDataId(1),
     read,
     Description("Number of Controllers.") : amended
    ] uint32 NumberControllers;

    //
    // Array of each controller's information.
    // Note that these are ULONGLONG aligned.
    //
    [WmiDataId(2),
     read,
     Description("Array of Controller Information Structures.") : amended,
     WmiSizeIs("NumberControllers")
    ] MPIO_CONTROLLER_INFO ControllerInfo[];

};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_控制器\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff562321)数据结构。 没有与此 WMI 类相关联的方法。

 

 





