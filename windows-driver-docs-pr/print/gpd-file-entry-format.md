---
title: GPD 文件项格式
description: GPD 文件项格式
ms.assetid: 44057b4d-5ea1-426f-ae87-047b650cbf65
keywords:
- GPD 文件条目 WDK Unidrv，格式
- 格式化 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a47b967392c63bde1b8d476a1003168e592219d6
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285088"
---
# <a name="gpd-file-entry-format"></a>GPD 文件项格式





所有 GPD 文件项都符合以下格式：

\***EntryName:EntryValue** {*GPD\_FileEntry，GPD\_FileEntry，...* }

*EntryName*始终是 UNIDRV 的 GPD parser 识别的预定义关键字，前面加上星号。

*EntryValue*必须是[GPD 值类型](gpd-value-types.md)之一。

每*个\_GPD FileEntry*都是另一个 GPD 文件条目，它符合上面所示的格式。 对于包含它的项的指定*EntryName* ，每个项都必须有效。

某些*EntryName*关键字不接受大括号或包含的子项。

每个 GPD 条目都按行尾或右大括号（ **}** ）结束。

下面的属性项是一个简单的 GPD 文件项（不接受子项）的示例：

```cpp
*MaxCopies: 99
```

此条目指定打印机可处理的最大副本数为99。

下面是一个更复杂的示例，描述了可以在两个页面方向（纵向或横向）中打印页面的打印机。 该示例还指定了驱动程序必须发送以选择每个方向的命令。

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

 

 




