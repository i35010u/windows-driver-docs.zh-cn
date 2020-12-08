---
title: 模拟字体命令
description: 模拟字体命令
keywords:
- 模拟字体命令 WDK Unidrv
- font 命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 880f9bedcd2dc318a20e64e1a87d811aea6a832f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797629"
---
# <a name="commands-for-simulated-fonts"></a>模拟字体命令





下表列出了用于控制模拟字体的命令。 所有命令都使用 [命令条目格式](command-entry-format.md)指定。

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
<td><p><strong>CmdBoldOff</strong></p></td>
<td><p>用于禁用粗体的命令。</p></td>
<td><p>可选。 如果指定了 <strong>CmdBoldOn</strong> ，则必须指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdBoldOn</strong></p></td>
<td><p>用于启用粗体的命令。</p></td>
<td><p>可选。 如果指定，Unidrv 将发送此命令以启用粗体并发送 <strong>CmdBoldOff</strong> 以禁用粗体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdClearAllFontAttribs</strong></p></td>
<td><p>用于禁用粗体、斜体和下划线功能的单个命令。</p></td>
<td><p>可选。 如果打印机支持粗体、斜体或下划线，则可以指定，但只支持使用单个命令禁用所有。 使用而不是 <strong>CmdBoldOff</strong>、 <strong>CmdItalicOff</strong> 和 <strong>CmdUnderlineOff</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdItalicOff</strong></p></td>
<td><p>要禁用斜体的命令。</p></td>
<td><p>可选。 如果指定了 <strong>CmdItalicOn</strong> ，则必须指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdItalicOn</strong></p></td>
<td><p>命令启用斜体。</p></td>
<td><p>可选。 如果已指定，Unidrv 将发送此命令以启用斜体并发送 <strong>CmdItalicOff</strong> 以禁用斜体。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectDoubleByteMode</strong></p></td>
<td><p>用于启用双字节打印的命令。</p></td>
<td><p>可选。 如果指定了 <strong>CmdSelectSingleByteMode</strong> ，则必须指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectSingleByteMode</strong></p></td>
<td><p>启用单字节打印的命令。</p></td>
<td><p>可选。 如果可以在单字节和双字节模式之间切换，则必须指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetFontSim</strong></p></td>
<td><p>用于设置粗体、斜体、下划线和删除线功能的单个命令。</p></td>
<td><p>可选。 如果在每次使用字体特性时必须设置字体特性 (对于不存储字体特性) 的打印机，则必须指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdStrikeThruOff</strong></p></td>
<td><p>用于禁用删除线的命令。</p></td>
<td><p>可选。 如果指定了 <strong>CmdStrikeThruOn</strong> ，则必须指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdStrikeThruOn</strong></p></td>
<td><p>用于启用删除线的命令。</p></td>
<td><p>可选。 如果指定此命令，Unidrv 将发送此命令以启用删除线并发送 <strong>CmdStrikeThruOff</strong> ，以禁用删除线。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdUnderlineOff</strong></p></td>
<td><p>用于禁用下划线的命令。</p></td>
<td><p>可选。 如果指定了 <strong>CmdUnderlineOn</strong> ，则必须指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdUnderlineOn</strong></p></td>
<td><p>启用下划线的命令。</p></td>
<td><p>可选。 如果指定此命令，Unidrv 将发送此命令以启用下划线并发送 <strong>CmdUnderlineOff</strong> 来禁用下划线。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdVerticalPrintingOff</strong></p></td>
<td><p>用于禁用垂直打印的命令。</p></td>
<td><p>可选。 如果指定了 <strong>CmdVerticalPrintingOn</strong> ，则必须指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdVerticalPrintingOn</strong></p></td>
<td><p>启用垂直打印的命令。</p></td>
<td><p>可选。 如果打印机支持垂直打印，则必须指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdWhiteTextOff</strong></p></td>
<td><p>用于禁用打印白色文本的命令。</p></td>
<td><p>可选。 如果指定了 <strong>CmdWhiteTextOn</strong> ，则必须指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdWhiteTextOn</strong></p></td>
<td><p>用于启用打印白色文本的命令。</p></td>
<td><p>可选。 如果指定此命令，Unidrv 将发送此命令以启用打印白文本，并发送 <strong>CmdWhiteTextOff</strong> 来禁用打印白色文本。 为了向后兼容 GPC 3.0，提供此命令 (。 ) </p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




