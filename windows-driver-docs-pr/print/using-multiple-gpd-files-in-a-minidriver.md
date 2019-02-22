---
title: 使用微型驱动程序中的多个 GPD 文件
description: 使用微型驱动程序中的多个 GPD 文件
ms.assetid: 2ec08b46-a286-4af8-a5d4-e0306f731b3f
keywords:
- GPD 文件 WDK Unidrv，多个
- 多个 GPD 文件 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8527a64aa417c2409ad31cf78e843dc61127bf31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540774"
---
# <a name="using-multiple-gpd-files-in-a-minidriver"></a>使用微型驱动程序中的多个 GPD 文件





Unidrv 微型驱动程序可以包含多个 GPD 文件。 这使您所共有的一个或多个 GPD 文件中的多个打印机位置特征，然后以包括这些常见 GPD 文件在特定打印机的单个 GPD 文件中。

若要包括其他 GPD 文件，请使用\*Include 指令中, 所述[预处理器指令](preprocessor-directives.md)。 可以使用多个\*Include 指令，如下面的示例中所示：

```cpp
*Include: "common1.gpd"
*Include: "common2.gpd"
*Include: "common3.gpd"
```

\*Include 指令 filename 参数不能是宏引用，并且不能包含路径说明。

每个包含的文件必须结尾的完整 GPD 文件条目，且该文件必须包含相同数量的左和右大括号。 包含的文件还可以包含\*Include 指令。

GPD 分析器将顶层 GPD 文件和所有包含的文件，就好像这是一个长文件。 因此，可以在随后包含的文件引用一个文件中定义的宏。 如果复制 GPD 文件条目，最近已分析的条目将替换以前的。 不重复的条目添加到 Unidrv 的数据库中。

 

 




