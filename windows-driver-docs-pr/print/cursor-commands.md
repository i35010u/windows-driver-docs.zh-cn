---
title: 光标命令
description: 光标命令
keywords:
- 打印机命令 WDK Unidrv，游标
- cursor 命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b7f4a529d18868730721c681d37808b54cdbb2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797433"
---
# <a name="cursor-commands"></a>光标命令





下表中的 [打印机命令](printer-commands.md) 将移动游标。 所有命令都使用 [命令条目格式](command-entry-format.md)指定。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令</th>
<th>描述</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CmdBackSpace</strong></p></td>
<td><p>用于将光标移回最后一个打印字符的命令。</p></td>
<td><p>可选。 仅用于 overstriking。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdCR</strong></p></td>
<td><p>将光标移动到最左侧 x 位置的命令。</p></td>
<td><p>必需。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdFF</strong></p></td>
<td><p>用于弹出页面的命令。</p></td>
<td><p>必需。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdLF</strong></p></td>
<td><p>命令将光标移到下一行。</p></td>
<td><p>必需。 移动量由 <strong>CmdSetLineSpacing</strong>指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdPopCursor</strong></p></td>
<td><p>命令从堆栈中弹出上次保存的游标位置。</p></td>
<td><p>如果指定了 <strong>CmdPushCursor</strong> ，则为必需。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdPushCursor</strong></p></td>
<td><p>用于将当前光标位置推送到堆栈上的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetAnyRotation</strong></p></td>
<td><p>用于将旋转方向设置为任意角度的命令 (以顺时针方向) 为单位。</p></td>
<td><p>可选。 如果不存在，打印机将不支持通过任意角度旋转。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetLineSpacing</strong></p></td>
<td><p>命令，用于设置发出 <strong>CmdLF</strong> 命令时光标移动的距离。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetSimpleRotation</strong></p></td>
<td><p>命令以逆时针方向以90度的倍数设置旋转角度。</p></td>
<td><p>可选。 如果打印机支持通过任意大小的角度进行旋转， <strong>CmdSetAnyRotation</strong> 命令可以替换此命令。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdUniDirectionOff</strong></p></td>
<td><p>用于禁用单向打印的命令，从而启用双向打印。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdUniDirectionOn</strong></p></td>
<td><p>用于启用单向打印的命令。</p></td>
<td><p>可选。 如果不存在，则以双向模式打印。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdXMoveAbsolute</strong></p></td>
<td><p>将光标移动到绝对 x 位置的命令。</p></td>
<td><p>可选。 命令字符串只能包含一个用于指定距离的标准变量。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdXMoveRelLeft</strong></p></td>
<td><p>命令从当前 x 位置将光标向左移动指定的量。</p></td>
<td><p>可选。 命令字符串只能包含一个用于指定距离的标准变量。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdXMoveRelRight</strong></p></td>
<td><p>命令从当前 x 位置将光标向右移动指定的量。</p></td>
<td><p>可选。 命令字符串只能包含一个用于指定距离的标准变量。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdYMoveAbsolute</strong></p></td>
<td><p>将光标移动到绝对 y 位置的命令。</p></td>
<td><p>可选。 命令字符串只能包含一个用于指定距离的标准变量。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdYMoveRelDown</strong></p></td>
<td><p>从当前 y 位置向下移动光标的命令（按指定的量）。</p></td>
<td><p>可选。 命令字符串只能包含一个用于指定距离的标准变量。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdYMoveRelUp</strong></p></td>
<td><p>从当前 y 位置向上移动光标的命令（按指定的量）。</p></td>
<td><p>可选。 命令字符串只能包含一个用于指定距离的标准变量。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




