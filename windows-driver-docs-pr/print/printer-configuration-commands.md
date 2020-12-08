---
title: 打印机配置命令
description: 打印机配置命令
keywords:
- 打印机命令 WDK Unidrv，配置
- 配置命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3381334552e95da8c1ca131970890dcc0107cda1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807353"
---
# <a name="printer-configuration-commands"></a>打印机配置命令





下表列出了打印机配置命令。 所有命令都使用 [命令条目格式](command-entry-format.md)指定。

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
<td><p>CmdStartJob</p></td>
<td><p>用于初始化打印作业的命令。</p></td>
<td><p>可选。 必须指定<a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>。</p></td>
</tr>
<tr class="even">
<td><p>CmdStartDoc</p></td>
<td><p>用于初始化文档的命令。</p></td>
<td><p>可选。 必须指定<a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CmdStartPage</p></td>
<td><p>命令初始化页面，并将光标位置设置为游标坐标 (0，0) 。</p></td>
<td><p>可选。 必须指定<a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndPage</p></td>
<td><p>用于完成打印页面的命令。</p></td>
<td><p>可选。 必须指定<a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CmdEndDoc</p></td>
<td><p>用于完成文档打印的命令。</p></td>
<td><p>可选。 必须指定<a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>。</p></td>
</tr>
<tr class="even">
<td><p>CmdEndJob</p></td>
<td><p>用于完成打印作业的命令。</p></td>
<td><p>可选。 必须指定<a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>。</p></td>
</tr>
<tr class="odd">
<td><p>CmdCopies</p></td>
<td><p>命令指定要打印的份数。</p></td>
<td><p>可选。 必须指定<a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>。</p></td>
</tr>
<tr class="even">
<td><p>CmdSleepTimeOut</p></td>
<td><p>命令，用于指定打印机在进入节能模式之前等待的分钟数。</p></td>
<td><p>可选。 必须指定<a href="command-execution-order.md" data-raw-source="[Command execution order](command-execution-order.md)">命令执行顺序</a>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




