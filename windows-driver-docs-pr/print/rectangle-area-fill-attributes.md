---
title: 矩形区域填充属性
description: 矩形区域填充属性
ms.assetid: 287e8805-4aec-490b-88da-00576a2f4fbf
keywords:
- 矩形区域填充属性 WDK Unidrv
- 填充矩形区域 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec00a61184bf4255ae64f1747ca673faf01321e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540776"
---
# <a name="rectangle-area-fill-attributes"></a>矩形区域填充属性





下表列出了属性描述用于填充矩形区域的打印机的支持。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>特性参数</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>CursorXAfterRectFill</strong></p></td>
<td><p>AT_RECT_X_ORIGIN 或 AT_RECT_X_END，指示位置光标&#39;填充的矩形区域，如打印机后 s x 坐标。</p></td>
<td><p>可选。 如果未指定，默认值将为 AT_RECT_X_ORIGIN。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CursorYAfterRectFill</strong></p></td>
<td><p>AT_RECT_Y_ORIGIN 或 AT_RECT_Y_END，指示位置光标&#39;填充的矩形区域，如打印机后 s y 坐标。</p></td>
<td><p>可选。 如果未指定，默认值将为 AT_RECT_Y_ORIGIN。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxGrayFill</strong></p></td>
<td><p>表示作为 CmdRectGrayFill 命令的参数允许的最大的灰色填充百分比的数字值。</p></td>
<td><p>可选。 如果未指定，默认值为 100 （百分比）。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinGrayFill</strong></p></td>
<td><p>表示作为 CmdRectGrayFill 命令的参数允许的最小的灰色填充百分比的数字值。</p></td>
<td><p>可选。 如果未指定，默认值为 1 （%）。</p></td>
</tr>
</tbody>
</table>

 

有关与打印机的矩形区域填充功能关联的命令的信息，请参阅[矩形区域填充命令](rectangle-area-fill-commands.md)。

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




