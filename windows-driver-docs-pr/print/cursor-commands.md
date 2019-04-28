---
title: 光标命令
description: 光标命令
ms.assetid: 3ef09c7e-0e88-4236-a4c9-d89eb7ec61cb
keywords:
- 打印机命令 WDK Unidrv，游标
- 光标的命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4825df7d9d8f129854e415c1ad3b05796ed09d54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349257"
---
# <a name="cursor-commands"></a>光标命令





[打印机命令](printer-commands.md)以下控制游标移动表中。 使用指定的所有命令[命令条目格式](command-entry-format.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Command</th>
<th>描述</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>CmdBackSpace</strong></p></td>
<td><p>将光标移回到打印的最后一个字符的命令。</p></td>
<td><p>可选。 仅用于 overstriking。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdCR</strong></p></td>
<td><p>若要将光标移到其最左边的 x 位置的命令。</p></td>
<td><p>必需。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdFF</strong></p></td>
<td><p>若要弹出一页的命令。</p></td>
<td><p>必需。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdLF</strong></p></td>
<td><p>将光标移到下一行的命令。</p></td>
<td><p>必需。 指定的移动量<strong>CmdSetLineSpacing</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdPopCursor</strong></p></td>
<td><p>若要弹出堆栈中的最后一个已保存的游标位置的命令。</p></td>
<td><p>需要<strong>CmdPushCursor</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdPushCursor</strong></p></td>
<td><p>若要将推送到堆栈上的当前光标位置的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetAnyRotation</strong></p></td>
<td><p>若要设置为 （以逆时针方向旋转的度数为单位） 的任意角度的旋转的命令。</p></td>
<td><p>可选。 如果不存在，则打印机不支持通过任意角度的旋转。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetLineSpacing</strong></p></td>
<td><p>命令的距离设置光标将移何时<strong>CmdLF</strong>发出命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSetSimpleRotation</strong></p></td>
<td><p>若要设置的倍数中逆时针方向旋转 90 度的旋转角度的命令。</p></td>
<td><p>可选。 如果打印机支持的任意大小的通过角度旋转<strong>CmdSetAnyRotation</strong>命令可以将此命令。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdUniDirectionOff</strong></p></td>
<td><p>若要禁用单向打印，从而支持双向打印的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdUniDirectionOn</strong></p></td>
<td><p>若要启用单向打印的命令。</p></td>
<td><p>可选。 如果不存在，在双向模式下打印。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdXMoveAbsolute</strong></p></td>
<td><p>若要将光标移到绝对的 x 位置的命令。</p></td>
<td><p>可选。 命令字符串可以包含仅有一个标准的变量，用于指定的距离。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdXMoveRelLeft</strong></p></td>
<td><p>若要将光标移到左侧当前的 x 位置，从指定的量的命令。</p></td>
<td><p>可选。 命令字符串可以包含仅有一个标准的变量，用于指定的距离。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdXMoveRelRight</strong></p></td>
<td><p>若要将光标向右移动当前的 x 位置，从指定的量的命令。</p></td>
<td><p>可选。 命令字符串可以包含仅有一个标准的变量，用于指定的距离。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdYMoveAbsolute</strong></p></td>
<td><p>若要将光标移到绝对的 y 位置的命令。</p></td>
<td><p>可选。 命令字符串可以包含仅有一个标准的变量，用于指定的距离。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdYMoveRelDown</strong></p></td>
<td><p>要将光标下移当前的 y 位置，从指定的量的命令。</p></td>
<td><p>可选。 命令字符串可以包含仅有一个标准的变量，用于指定的距离。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdYMoveRelUp</strong></p></td>
<td><p>要上移光标当前的 y 位置，从指定的量的命令。</p></td>
<td><p>可选。 命令字符串可以包含仅有一个标准的变量，用于指定的距离。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




