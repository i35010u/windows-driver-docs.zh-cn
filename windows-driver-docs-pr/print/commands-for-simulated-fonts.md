---
title: 模拟字体命令
description: 模拟字体命令
ms.assetid: 3bfdcf86-35ac-4b95-9efd-31f79a8b9871
keywords:
- 模拟的字体命令 WDK Unidrv
- 字体的命令 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc65447889349cf1071c4bb64654a005062c146
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355897"
---
# <a name="commands-for-simulated-fonts"></a>模拟字体命令





下表列出了用于控制模拟的字体的命令。 使用指定的所有命令[命令条目格式](command-entry-format.md)。

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
<td><p><strong>CmdBoldOff</strong></p></td>
<td><p>若要禁用粗体的命令。</p></td>
<td><p>可选。 如果必须指定<strong>CmdBoldOn</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdBoldOn</strong></p></td>
<td><p>若要启用粗体的命令。</p></td>
<td><p>可选。 如指定，则 Unidrv 发送此命令以启用粗体并将其发送<strong>CmdBoldOff</strong>禁用粗体设置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdClearAllFontAttribs</strong></p></td>
<td><p>若要禁用粗体、 斜体和下划线功能的单个命令。</p></td>
<td><p>可选。 可以指定是否打印机支持粗体、 斜体或下划线，但支持只能有一个命令禁用其全部。 而不是使用<strong>CmdBoldOff</strong>， <strong>CmdItalicOff</strong>并<strong>CmdUnderlineOff</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdItalicOff</strong></p></td>
<td><p>若要禁用斜体显示的命令。</p></td>
<td><p>可选。 如果必须指定<strong>CmdItalicOn</strong>指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdItalicOn</strong></p></td>
<td><p>若要启用斜体显示的命令。</p></td>
<td><p>可选。 如指定，则 Unidrv 发送此命令以启用斜体并将其发送<strong>CmdItalicOff</strong>禁用斜体。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectDoubleByteMode</strong></p></td>
<td><p>若要启用双字节打印的命令。</p></td>
<td><p>可选。 如果必须指定<strong>CmdSelectSingleByteMode</strong>指定。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectSingleByteMode</strong></p></td>
<td><p>若要启用单字节打印的命令。</p></td>
<td><p>可选。 必须指定是否打印机可以单字节和双字节模式之间切换。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSetFontSim</strong></p></td>
<td><p>单个命令设置粗体、 斜体、 下划线、 和线的功能。</p></td>
<td><p>可选。 必须指定是否必须设置的字体特征 （适用于不存储字体特征的打印机） 每次使用的字体。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdStrikeThruOff</strong></p></td>
<td><p>若要禁用删除线的命令。</p></td>
<td><p>可选。 如果必须指定<strong>CmdStrikeThruOn</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdStrikeThruOn</strong></p></td>
<td><p>若要启用删除线的命令。</p></td>
<td><p>可选。 如果指定，Unidrv 发送此命令以启用删除线，并将发送<strong>CmdStrikeThruOff</strong>禁用删除线。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdUnderlineOff</strong></p></td>
<td><p>若要禁用的下划线的命令。</p></td>
<td><p>可选。 如果必须指定<strong>CmdUnderlineOn</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdUnderlineOn</strong></p></td>
<td><p>若要启用的下划线的命令。</p></td>
<td><p>可选。 如指定，则 Unidrv 发送此命令以启用加下划线并将其发送<strong>CmdUnderlineOff</strong>若要禁用的下划线。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdVerticalPrintingOff</strong></p></td>
<td><p>若要禁用垂直打印的命令。</p></td>
<td><p>可选。 如果必须指定<strong>CmdVerticalPrintingOn</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdVerticalPrintingOn</strong></p></td>
<td><p>若要启用垂直打印的命令。</p></td>
<td><p>可选。 必须指定打印机是否支持垂直打印。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdWhiteTextOff</strong></p></td>
<td><p>要禁用打印白色文本的命令。</p></td>
<td><p>可选。 如果必须指定<strong>CmdWhiteTextOn</strong>指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdWhiteTextOn</strong></p></td>
<td><p>启用打印白色文本的命令。</p></td>
<td><p>可选。 如果指定，Unidrv 发送此命令以启用打印白色文本，并将发送<strong>CmdWhiteTextOff</strong>禁用打印白色文本。 （此命令用于向后与 GPC 3.0 兼容性。）</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




