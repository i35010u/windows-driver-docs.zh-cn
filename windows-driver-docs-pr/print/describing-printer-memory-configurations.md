---
title: 描述打印机内存配置
description: 描述打印机内存配置
ms.assetid: 4a85788a-9713-42fb-a788-4d45f9aaabac
keywords:
- Unidrv，打印机内存配置
- GPD 文件 WDK Unidrv，打印机内存配置
- 打印机内存配置 WDK Unidrv
- 内存配置 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ce5a5c887787cbdc0ae2ee997e135170e91bb36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566108"
---
# <a name="describing-printer-memory-configurations"></a>描述打印机内存配置





Unidrv 微型驱动程序可以包含打印机的好和默认内存配置的说明，以便可以尝试 Unidrv 来跟踪打印机内存使用情况。 每个内存配置说明包括内存总量和可用内存的值。 可用内存可用于下载字体，保护页面和由 Unidrv 控制其他操作。

在 GPD 文件中，可以使用两种方法来描述打印机的可能的内存配置。 这两种方法涉及指定属性中的\*功能的内存功能，这是一个条目的[标准功能](standard-features.md)。 两种方法是按如下所示：

1.  可以在单独指定每个可能的配置\*选项中的条目\*功能条目。 每个\*选项该项必须包含\*MemoryConfigKB 属性中所述[内存功能的选项属性](option-attributes-for-the-memory-feature.md)。

    例如，若要指定打印机可以有两个内存配置、 可用 450 千字节为单位的 1 兆字节配置和可用 1350 千字节为单位的 2 兆字节配置，可以使用以下 GPD 条目：

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

2.  或者，\*功能条目可包含一个或多个\*MemConfigKB 或\*MemConfigMB 特性而不是\*选项条目。 这是只是一个指定内存选项而不包括一组方法\*选项条目。 每个\*MemConfigKB 或\*MemConfigMB 属性表示内存选项。

    例如，若要使用可用 1350 千字节为单位指定相同的两个配置、 可用 450 千字节为单位的 1 兆字节配置和 2 兆字节配置，可以使用以下 GPD 条目：

    ```cpp
    *Feature: Memory
    {
        *Name: "Printer Memory"
        *DefaultOption: 1024KB
        *MemConfigKB: PAIR(1024, 450)
        *MemConfigKB: PAIR(2048, 1350)
    }
     
    ```

    GPD 分析器创建每个配置，根据对语句中的第一项可显示的选项名称。 在此示例中，选项名称将是"1024 KB"和"2048 KB"。 参数\*DefaultOption 属性必须与这些名称之一匹配。

方法 1 和 2 方法可在单个内使用\*功能条目。

如果分析器生成的选项名称与本地化要求不兼容，请使用方法 1 而不是方法 2。

无论您使用哪种方法[Unidrv 用户界面](unidrv-user-interface.md)显示设备的打印机属性表中的内存功能选项。

如果你的微型驱动程序指定内存配置，它还可以指定可以在打印机内存中存储和其可用空间用完的数据类型。 \*MemoryUsage 属性是之一[打印机功能特性](printer-capability-attributes.md)，并可用来向 Unidrv 指示字体，光栅，矢量数据或的三个组合都存储在打印机内存。 指定每种类型，对于 Unidrv 尝试跟踪的打印机的内存量正在使用中。

 

 




