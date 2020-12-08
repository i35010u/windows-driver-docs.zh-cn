---
title: 块宏
description: 块宏
keywords:
- 阻止宏 WDK GPD 文件
- 引用宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa2cf97521c65a27695cf9635f95dd5491a21dbe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797777"
---
# <a name="block-macros"></a>块宏





块宏用于分隔要反复插入到 GPD 文件中的一组 GPD 文件项。 可以在块宏定义中包含任何项类型，如功能和选项语句、特性规范以及对值宏或其他块宏的引用。

以下规则适用于使用块宏：

-   GPD 文件中的块宏定义必须位于任何引用之前。

-   在根级别定义的块宏 (即，不在大括号) 可通过定义它的 GPD 文件提供。 否则，block 宏的作用域是包含其定义的左大括号和右大括号集。

-   块宏定义可以包含其他块宏和值宏的定义。

-   块宏定义可以引用以前定义的其他块宏和值宏，但它不能引用自身。

-   块宏不接受参数。

-   如果在宏体中包括大括号，则它们必须成对 (也就是说，) 左括号和右大括号的数目必须相等。

-   如果创建两个具有相同名称的块宏，则第一个定义将生效，直到 GPD 分析器遇到第二个定义。 然后，第二个定义将替换第一个。 如果第二个定义的作用域结束，则会恢复第一个定义。

### <a name="block-macro-format"></a>块宏格式

若要在 GPD 文件中定义块宏，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>BlockMacro</strong>： <em>BlockMacroName</em> {<em>BlockMacroBody</em>}</p></td>
</tr>
</tbody>
</table>

 

其中， *BlockMacroName* 是唯一的名称， *BlockMacroBody* 是一个或多个 [GPD 文件条目](gpd-file-entries.md)的集合。 如果 *BlockMacroBody* 包含大括号，则必须包含等号左括号和右大括号 ( {，} ) 。

例如，可以定义名为 EnvelopeDefaults 的块宏，定义如下：

```cpp
*BlockMacro: EnvelopeDefaults
{
    *PrintableArea: PAIR(4646, 6738)
    *PrintableOrigin: PAIR(150, 150)
    *RotateSize: TRUE
}
```

### <a name="referencing-block-macros"></a>引用块宏

若要引用块宏，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* InsertBlock</strong>： = BlockMacroName</p></td>
</tr>
</tbody>
</table>

 

其中 *BlockMacroName* 是一个唯一名称，以前在定义宏的 **\* BlockMacro** 项中指定。

例如，若要在选项规范内引用 EnvelopeDefaults 宏，可以使用以下项：

```cpp
*Option: Env9
{
    *InsertBlock: =EnvelopeDefaults
}
```

 

 




