---
title: 自定义功能
description: 自定义功能
keywords:
- 打印机功能 WDK Unidrv，自定义
- 自定义打印机功能 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58421954750d8197b3ae1d7c9f8f10aecc03f060
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797413"
---
# <a name="customized-features"></a>自定义功能





自定义功能是特定于硬件的功能。 为这些功能创建唯一名称。 对于每个自定义功能，必须指定一组 [自定义选项](customized-options.md)。 例如，假设您的打印机提供经济模式的操作。 由于 GPD 语言不提供用于描述此功能的功能，因此必须定义自定义功能及其选项。 此功能的规范可能如下所示：

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

 

 




