---
title: 描述打印机内存配置
description: 描述打印机内存配置
keywords:
- Unidrv，打印机内存配置
- GPD 文件 WDK Unidrv，打印机内存配置
- 打印机内存配置 WDK Unidrv
- 内存配置 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e785a2ebf3d79ad45582e6ce47d1ac606a06c32a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797287"
---
# <a name="describing-printer-memory-configurations"></a>描述打印机内存配置





Unidrv 微型驱动程序可以包含打印机的可能和默认内存配置的说明，以便 Unidrv 可以尝试跟踪打印机内存使用量。 每个内存配置说明都包括内存总量和可用内存的值。 可用内存可用于下载字体、保护页面和由 Unidrv 控制的其他操作。

在 GPD 文件中，可以使用两种方法来描述打印机的可能内存配置。 这两种方法都涉及在 \* 内存功能的功能条目中指定属性，这是一项 [标准功能](standard-features.md)。 这两种方法如下所示：

1.  可以在功能条目中的单独选项条目中指定每个可能的配置 \* \* 。 每个 \* 选项条目都必须包含 \* MemoryConfigKB 属性，该属性在 [内存功能的选项属性](option-attributes-for-the-memory-feature.md)中进行了介绍。

    例如，若要指定打印机可以具有两个内存配置，可使用 450 kb 的 1 mb 配置和 2 mb 的配置（可用 1350 kb），可以使用以下 GPD 项：

    ```cpp
    *Feature: Memory
    {
        *Name: "Printer Memory"
        *DefaultOption: 1MB
        *Option: 1MB
        {
            *Name: "Standard 1MB"
            *MemoryConfigKB: PAIR(1024, 450)
        }
        *Option: 2MB 
        {
            *Name: "Add-On 2MB"
            *MemoryConfigKB: PAIR(2048,1350)
        }
    }
     
    ```

2.  或者， \* 功能条目可以包含一个或多个 \* MemConfigKB 或 \* MemConfigMB 属性，而不是 \* 选项条目。 这只是一种方法，用于指定内存选项，而无需包括一组 \* 选项项。 每个 \* MemConfigKB 或 \* MemConfigMB 属性表示一个内存选项。

    例如，若要指定相同的两个配置，可使用 450 kb 的 1 mb 配置和 2 mb 的配置（可用 1350 kb），可以使用以下 GPD 项：

    ```cpp
    *Feature: Memory
    {
        *Name: "Printer Memory"
        *DefaultOption: 1024KB
        *MemConfigKB: PAIR(1024, 450)
        *MemConfigKB: PAIR(2048, 1350)
    }
     
    ```

    GPD 分析器基于对语句中的第一项，为每个配置创建一个可显示的选项名称。 在此示例中，选项名称为 "1024KB" 和 "2048KB"。 DefaultOption 属性的参数 \* 必须与其中一个名称匹配。

方法1和方法2都可以在单个 \* 功能条目中使用。

如果分析器生成的选项名称与本地化要求不兼容，请使用方法1而不是方法2。

无论使用哪种方法， [Unidrv 用户界面](unidrv-user-interface.md) 都会在设备的打印机属性表中显示内存功能选项。

如果你的微型驱动程序指定内存配置，它还可以指定可存储在打印机内存中的数据类型，并占用其可用空间。 \*MemoryUsage 属性是一个[打印机功能属性](printer-capability-attributes.md)，您可以使用它来指示 Unidrv 字体、光栅、矢量数据或这三个数据是否存储在打印机内存中。 对于指定的每种类型，Unidrv 将尝试跟踪使用的打印机内存量。

 

 




