---
title: 块宏
description: 块宏
ms.assetid: da2f6161-072a-4d3c-94a8-1020520de524
keywords:
- 块宏 WDK GPD 文件
- 引用宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2907bf99f495a6a691acbeeb876bbec24f3bbf83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523183"
---
# <a name="block-macros"></a>块宏





块宏用于分隔的一组你想要重复插入 GPD 文件的 GPD 文件项。 可以在块宏定义中，如功能和选项语句、 属性规范和值宏或其他块宏引用包含任何条目类型。

以下规则适用于使用的块宏：

-   块宏定义中 GPD 文件必须位于之前对它的任何引用。

-   在根级别定义的块宏 (即，而不是在大括号) 可通过定义它，它定义之后的 GPD 文件。 否则，块宏的作用域是包含其定义的左和右大括号的组。

-   块宏定义可以包含其他块宏和值宏的定义。

-   块宏定义可以引用其他块之前定义的宏和值宏，但它不能引用自身。

-   块宏不接受参数。

-   如果宏正文中包含大括号，它们必须成对使用 （也就是说，必须有相同数目的左和右大括号）。

-   如果具有相同名称创建两个块宏，第一个定义实际上是，直到 GPD 分析器遇到第二个定义。 第二个定义，然后将替换第一个。 如果第二个定义的作用域结束时，恢复过程的第一个定义。

### <a name="block-macro-format"></a>块宏格式

若要在 GPD 文件中定义块宏，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>BlockMacro</strong>:<em>BlockMacroName</em> {<em>BlockMacroBody</em>}</p></td>
</tr>
</tbody>
</table>

 

其中*BlockMacroName*是唯一的名称，并*BlockMacroBody*是一组的一个或多个[GPD 文件条目](gpd-file-entries.md)。 如果*BlockMacroBody*包含大括号必须包含相同数量的左和右大括号 （{，}）。

例如，可能会定义一个名为 EnvelopeDefaults，按以下方式定义的块宏：

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
<td><p><strong>* InsertBlock</strong>: = BlockMacroName</p></td>
</tr>
</tbody>
</table>

 

其中*BlockMacroName*是唯一的名称，在以前指定 **\*BlockMacro**定义宏的条目。

例如，若要引用中的选项规范 EnvelopeDefaults 宏，可以使用以下项：

```cpp
*Option: Env9
{
    *InsertBlock: =EnvelopeDefaults
}
```

 

 




