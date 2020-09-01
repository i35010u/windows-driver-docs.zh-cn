---
title: MPIO \_ 控制器 \_ 配置 WMI 类
description: MPIO \_ 控制器 \_ 配置 WMI 类
ms.assetid: c11429d6-b016-464e-a7b4-03b6cdc8ddb7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3a78d551e33d10f6b16ff0f0d3332be4b3a49c43
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191289"
---
# <a name="mpio_controller_configuration-wmi-class"></a>MPIO \_ 控制器 \_ 配置 WMI 类


WMI 客户端使用 MPIO \_ 控制器 \_ 配置 WMI 类来查询 MPIO，以了解有关附加到系统的存储控制器的信息。

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

当 WMI 工具套件编译此类定义时，它将生成 [**MPIO \_ 控制器 \_ 配置**](/windows-hardware/drivers/ddi/mpiowmi/ns-mpiowmi-_mpio_controller_configuration) 数据结构。 没有与此 WMI 类相关联的方法。

 

