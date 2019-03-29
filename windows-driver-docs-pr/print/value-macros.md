---
title: 值宏
description: 值宏
ms.assetid: 265b2d35-5e91-4c47-a145-1e9f8c497c2c
keywords:
- 值宏 WDK GPD 文件
- 引用宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9911ddbd5c1638367dc204bcf03eaa1ec0ad3fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576338"
---
# <a name="value-macros"></a>值宏





值宏用于指定一组你想要单独插入的一个或多个值，包括反复 GPD 文件。 值可以是任意[GPD 值类型](gpd-value-types.md)。

以下规则适用于使用的值宏：

-   值宏定义中 GPD 文件必须位于之前对它的任何引用。

-   在根级别定义的值宏 (即，而不是在大括号) 可通过定义它，它定义之后的 GPD 文件。 否则，值宏的作用域是包含其定义的左和右大括号的组。

-   值宏必须解析为之一[GPD 值类型](gpd-value-types.md)。

-   如果所有值都是文本字符串，但值宏不能引用自身，值宏定义可以引用其他以前定义的值的宏。

-   值宏不接受参数。

-   如果具有相同名称创建两个值宏，第一个定义实际上是，直到 GPD 分析器遇到第二个定义。 第二个定义，然后将替换第一个。 如果第二个定义的作用域结束时，恢复过程的第一个定义。

### <a name="value-macro-format"></a>值宏格式

若要在 GPD 文件中定义一个或多个值宏，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* 宏：<em>ValueMacroGroupName</em> { <em>ValueMacroBody</em> }</p></td>
</tr>
</tbody>
</table>

 

其中*ValueMacroGroupName*是唯一的名称，并*ValueMacroBody*一组唯一的值名称和关联的值，如下所示：

*ValueMacroName* :*MacroValue*

其中*ValueMacroName*是唯一的宏的名称，并*MacroValue*表示[GPD 值类型](gpd-value-types.md)。 (*MacroValue* ，只要已解析的字符串表示 GPD 值类型可以包括对以前定义的值宏的引用。)

例如，可能会按如下所示定义一组常用的命令前缀的值宏：

```cpp
*Macros: HP4L
{
    LetterCmdPrefix: "<1B>&l2a8c1E<1B>*p0x0Y"
    A4CmdPrefix: "<1B>&l26a8c1E<1B>*p0x0Y"
    Env10CmdPrefix: "<1B>&l81a8c1E<1B>*p0x0Y"
}
```

请注意， *ValueMacroGroupName* (HP4L 在示例中) 是可选的处理为注释。

### <a name="referencing-value-macros"></a>引用值宏

若要引用值宏，请使用以下格式：

= *ValueMacroName*

其中*ValueMacroName*是唯一的名称，在以前指定\*定义宏的宏条目。

例如，为其中一个 HP4L 宏命令规范中的引用，可以使用以下项：

```cpp
*Command: CmdSelect
{
    *Cmd: =LetterCmdPrefix "<1B>*c0t5760x7680Y"
}
```

可以通过将宏引用结合起来使用 nonmacro 值赋值的时，才是当所有的宏定义和其他值表示文本或命令的子字符串，该示例中所示。 在所有其他情况下，宏引用必须代表要分配的整个值。

 

 




