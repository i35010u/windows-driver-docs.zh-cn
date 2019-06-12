---
title: 注释和已忽略的块
description: 注释和已忽略的块
ms.assetid: 8b3a0195-b2c8-491d-abcd-bfaebefbc77d
keywords:
- GPD 文件条目 WDK Unidrv，已忽略的块
- 忽略块 WDK GPD 文件
- GPD 文件条目 WDK Unidrv，注释
- 注释 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5ec203052bfbd6368228c32786f28138342ff09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382611"
---
# <a name="comments-and-ignored-blocks"></a>注释和已忽略的块





GPD 文件可以包含注释。 对于注释的格式如下所示：

**\*%** *CommentString*

其中*CommentString*是结尾行结束符的字符的任何字符串。 每个行的多行注释必须以开头 **\* %** 字符序列。 **\* %** 前面的序列必须由空格或换行符。

以下是有效注释的示例：

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

若要请求 GPD 分析器忽略 GPD 条目的组，可以创建包含要忽略的项的已忽略的块。 已忽略的块的格式如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>*IgnoreBlock</strong> { <em>IgnoredEntries</em> }</p></td>
</tr>
</tbody>
</table>

 

其中*IgnoredEntries*是一套 GPD 文件条目，其中包含相同数目的左和右大括号。

在以下示例中，GPD 分析器将忽略描述横向 GPD 条目\_CC90 选项。

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

 

 




