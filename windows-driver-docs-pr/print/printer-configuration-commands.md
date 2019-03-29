---
title: 打印机配置命令
description: 打印机配置命令
ms.assetid: ed5102e7-1651-4188-8042-f0d544a54a1d
keywords:
- 打印机命令 WDK Unidrv、 配置
- 配置命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab87b04eac3c5bbfce2bdd4c481c5e3e2461972
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569071"
---
# <a name="printer-configuration-commands"></a>打印机配置命令





下表列出了打印机配置命令。 使用指定的所有命令[命令条目格式](command-entry-format.md)。

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
<td><p>CmdStartJob</p></td>
<td><p>若要初始化的打印作业的命令。</p></td>
<td><p>可选。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>必须指定。</p></td>
</tr>
<tr class="even">
<td><p>CmdStartDoc</p></td>
<td><p>若要初始化文档的命令。</p></td>
<td><p>可选。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>必须指定。</p></td>
</tr>
<tr class="odd">
<td><p>CmdStartPage</p></td>
<td><p>要初始化页面并将设置为 (0，0) 光标坐标中的光标位置的命令。</p></td>
<td><p>可选。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>必须指定。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndPage</p></td>
<td><p>若要完成打印页的命令。</p></td>
<td><p>可选。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>必须指定。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEndDoc</p></td>
<td><p>若要完成打印文档的命令。</p></td>
<td><p>可选。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>必须指定。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndJob</p></td>
<td><p>若要完成打印作业的命令。</p></td>
<td><p>可选。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>必须指定。</p></td>
</tr>
<tr class="odd">
<td><p>CmdCopies</p></td>
<td><p>若要指定要打印的份数的命令。</p></td>
<td><p>可选。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>必须指定。</p></td>
</tr>
<tr class="even">
<td><p>CmdSleepTimeOut</p></td>
<td><p>命令指定的打印机进入节能模式之前要等待的分钟数。</p></td>
<td><p>可选。 <a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>必须指定。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




