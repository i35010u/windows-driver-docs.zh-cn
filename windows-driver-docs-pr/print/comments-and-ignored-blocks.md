---
title: 注释和已忽略的块
description: 注释和已忽略的块
keywords:
- GPD 文件条目 WDK Unidrv，已忽略块
- 已忽略块 WDK GPD 文件
- GPD 文件条目 WDK Unidrv，评论
- 注释 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4363af681eca7467c3abe80f7812165a27a1ebf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797631"
---
# <a name="comments-and-ignored-blocks"></a>注释和已忽略的块





GPD 文件可以包含注释。 注释的格式如下所示：

**\*%***CommentString*

其中， *CommentString* 是以行终止符结尾的任意字符串。 多行注释的每一行必须以 **\*%** 字符序列开头。 **\*%** 序列的前面必须是空格或换行符。

下面是有效注释的示例：

```cpp
*% This section of the GPD file
*% contains macro definitions.
*Macros: HP4L
{
    *% These macros define command prefixes for the paper size feature.
    LetterCmdPrefix: "<1B>&l2a8c1E<1B>*p0x0Y"  *% Prefix for letter option.
    A4CmdPrefix: "<1B>&l26a8c1E<1B>*p0x0Y"     *% Prefix for A4 option.
    Env10CmdPrefix: "<1B>&l81a8c1E<1B>*p0x0Y"  *% Prefix for Env10 option.
}
```

若要请求 GPD 分析器忽略一组 GPD 项，可以创建一个包含要忽略的项的忽略块。 已忽略的块的格式如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* IgnoreBlock</strong> { <em>IgnoredEntries</em> }</p></td>
</tr>
</tbody>
</table>

 

其中， *IgnoredEntries* 是一组 GPD 文件项，其中包含相等的左大括号和右大括号。

在下面的示例中，GPD 分析器将忽略描述横向 CC90 选项的 GPD 条目 \_ 。

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
*IgnoreBlock
{
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
}
```

 

 




