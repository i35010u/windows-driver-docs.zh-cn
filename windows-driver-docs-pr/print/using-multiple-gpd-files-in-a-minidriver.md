---
title: 在微型驱动程序中使用多个 GPD 文件
description: 在微型驱动程序中使用多个 GPD 文件
keywords:
- GPD files WDK Unidrv，多个
- 多个 GPD 文件 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab3317a3bbc5099cd4b0448d5dcab15309886d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835425"
---
# <a name="using-multiple-gpd-files-in-a-minidriver"></a>在微型驱动程序中使用多个 GPD 文件





Unidrv 微型驱动程序可包含多个 GPD 文件。 这样，你就可以将多个打印机共用的特性放置在一个或多个 GPD 文件中，然后将这些常见的 GPD 文件包含在特定打印机的单个 GPD 文件中。

若要包含其他 GPD 文件，请使用 \* [预处理器指令](preprocessor-directives.md)中介绍的 include 指令。 可以使用多个 \* Include 指令，如以下示例中所示：

```cpp
*Include: "common1.gpd"
*Include: "common2.gpd"
*Include: "common3.gpd"
```

\*Include 指令的 filename 参数不能是宏引用，并且不能包含路径规范。

每个包含的文件必须以完整的 GPD 文件项结束，并且该文件必须包含等号左括号和右大括号。 包含的文件还可以包含 \* Include 指令。

GPD 分析器将顶级 GPD 文件和所有包含的文件视为一个长文件。 因此，在一个文件中定义的宏可以在随后包含的文件中引用。 如果复制了 GPD 文件项，则最新分析的条目将替换以前的条目。 不重复的条目将添加到 Unidrv 的数据库中。

 

 




