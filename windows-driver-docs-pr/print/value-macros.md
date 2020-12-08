---
title: 值宏
description: 值宏
keywords:
- 值宏 WDK GPD 文件
- 引用宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ffedb83e8f2c5eb22eef100084c31444e95be11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785852"
---
# <a name="value-macros"></a>值宏





值宏用于指定要在 GPD 文件中单独和重复插入的一个或多个值的集合。 值可以是任何 [GPD 值类型](gpd-value-types.md)。

以下规则适用于值宏的使用：

-   GPD 文件中的值宏定义必须位于引用它之前。

-   在根级别定义的值宏 (即，不在大括号) 中，可以通过定义它的 GPD 文件来使用。 否则，值宏的作用域是包含其定义的左大括号和右大括号集。

-   值宏必须解析为 [GPD 值类型](gpd-value-types.md)之一。

-   如果所有值都是文本字符串，则值宏定义可以引用以前定义的其他值宏，但值宏无法引用其自身。

-   值宏不接受参数。

-   如果创建两个具有相同名称的值宏，则第一个定义将生效，直到 GPD 分析器遇到第二个定义。 然后，第二个定义将替换第一个。 如果第二个定义的作用域结束，则会恢复第一个定义。

### <a name="value-macro-format"></a>值宏格式

若要在 GPD 文件中定义一个或多个值宏，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* 宏： <em>ValueMacroGroupName</em> { <em>ValueMacroBody</em> }</p></td>
</tr>
</tbody>
</table>

 

其中， *ValueMacroGroupName* 是唯一的名称， *ValueMacroBody* 是一组唯一的值名称和关联的值，如下所示：

*ValueMacroName* ： *MacroValue*

其中， *ValueMacroName* 是唯一的宏名称， *MacroValue* 表示 [GPD 值类型](gpd-value-types.md)。  (*MacroValue* 可以包括对以前定义的值宏的引用，前提是解析后的字符串表示 GPD 值类型。 ) 

例如，可以为一组常用的命令前缀定义值宏，如下所示：

```cpp
*Macros: HP4L
{
    LetterCmdPrefix: "<1B>&l2a8c1E<1B>*p0x0Y"
    A4CmdPrefix: "<1B>&l26a8c1E<1B>*p0x0Y"
    Env10CmdPrefix: "<1B>&l81a8c1E<1B>*p0x0Y"
}
```

请注意，示例) 中的 *ValueMacroGroupName* (HP4L 是可选的，并被视为注释。

### <a name="referencing-value-macros"></a>引用值宏

若要引用值宏，请使用以下格式：

= *ValueMacroName*

其中 *ValueMacroName* 是一个唯一名称，以前在 \* 定义宏的 Macros 项中指定。

例如，若要在命令规范内引用其中一个 HP4L 宏，可以使用以下项：

```cpp
*Command: CmdSelect
{
    *Cmd: =LetterCmdPrefix "<1B>*c0t5760x7680Y"
}
```

仅当所有宏定义和其他值都表示文本或命令子字符串时，才可以通过结合宏引用和 nonmacro 值来分配值，如示例中所示。 在所有其他情况下，宏引用必须表示要分配的整个值。

 

 




