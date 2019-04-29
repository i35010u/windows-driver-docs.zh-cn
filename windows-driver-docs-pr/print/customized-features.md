---
title: 自定义功能
description: 自定义功能
ms.assetid: a7dfed02-3505-4ed6-86cf-efb273f76ad6
keywords:
- 打印机功能 WDK Unidrv，自定义
- 自定义的打印机功能 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9480f1b71049959ec1d6f5621292fdd7d2cfa76
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365548"
---
# <a name="customized-features"></a>自定义功能





自定义的功能是特定于您的硬件。 创建这些功能的唯一名称。 对于每个自定义功能，必须指定一系列[自定义选项](customized-options.md)。 例如，假设您的打印机提供操作的另一经济模式。 因为 GPD 语言不提供用于描述此功能的一项功能，必须定义自定义的功能和其自己的选项。 功能的规范可能会出现，如下所示：

```cpp
*Feature: EconoMode
{
    *Name: "Economy Mode"
    *FeatureType: PRINTER_PROPERTY
    *DefaultOption: EconoModeOff
    *Option: EconoModeOff
    {
        *Name: "Off"
        *Command: CmdSelect
         {
             *Order: DOC_SETUP.5
             *Cmd: "@PJL SET ECONOMODE=OFF<0A>"
         }
    }
    *Option: EconoModeOn
    {
        *Name: "On"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.5
            *Cmd: "@PJL SET ECONOMODE=ON<0A>"
        }
    }
}
```

 

 




