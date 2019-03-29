---
title: GPD 文件项格式
description: GPD 文件项格式
ms.assetid: 44057b4d-5ea1-426f-ae87-047b650cbf65
keywords:
- GPD 文件条目 WDK Unidrv，格式
- WDK GPD 文件格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 053581ba1a6e0ca48a780e3d82b8ffab649b2bc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562135"
---
# <a name="gpd-file-entry-format"></a>GPD 文件项格式





所有 GPD 文件条目都符合以下格式：

**\\*** <em>EntryName</em>**:***EntryValue* **{**<em>GPD\_FileEntry, GPD\_FileEntry, ...</em>**}**

*EntryName*始终 Unidrv 的 GPD 分析器识别，一个预定义的关键字前面标有星号。

*EntryValue*必须是一个[GPD 值类型](gpd-value-types.md)。

每个*GPD\_FileEntry*是另一个 GPD 文件条目，符合上面所示的格式。 每个这些子项必须是有效的指定*EntryName*的包含它的条目。

某些*EntryName*关键字不接受大括号或包含的子项。

每个 GPD 条目终止行尾或右大括号 ( **}** )。

不接受子项，一个简单 GPD 文件条目的一个示例是以下属性条目：

```cpp
*MaxCopies: 99
```

此项指定打印机可以处理的副本的最大数目为 99。

下面是更复杂的示例中，描述打印机可以打印页面中的两个页面方向 （纵向或横向）。 该示例还指定驱动程序必须发送以选择每个方向的命令。

```cpp
*Feature: Orientation
{
    *Name: "Orientation"
    *DefaultOption: Portrait
    *Option: Portrait
    {
        *Name: "Portrait"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.7
            *Cmd: "<1B>&l0O"
        }
    }
    *Option: LANDSCAPE_CC90
    {
        *Name: "Landscape"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.7
            *Cmd: "<1B>&l1O"
        }
    }
}
```

 

 




