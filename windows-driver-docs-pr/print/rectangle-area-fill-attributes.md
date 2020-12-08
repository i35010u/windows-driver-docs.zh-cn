---
title: 矩形区域填充属性
description: 矩形区域填充属性
keywords:
- 矩形区域填充属性 WDK Unidrv
- 填充矩形区域 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d5b7d40b28ed52fec80b31bce847c716af9d2b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807067"
---
# <a name="rectangle-area-fill-attributes"></a>矩形区域填充属性





下表列出了说明打印机对填充矩形区的支持的属性。

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
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>CursorXAfterRectFill</strong></p></td>
<td><p>AT_RECT_X_ORIGIN 或 AT_RECT_X_END，指示在打印机填充矩形区域后光标的 X 坐标位置。</p></td>
<td><p>可选。 如果未指定，则默认值为 AT_RECT_X_ORIGIN。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>CursorYAfterRectFill</strong></p></td>
<td><p>AT_RECT_Y_ORIGIN 或 AT_RECT_Y_END，指示在打印机填充矩形区域后光标的 Y 坐标位置。</p></td>
<td><p>可选。 如果未指定，则默认值为 AT_RECT_Y_ORIGIN。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>MaxGrayFill</strong></p></td>
<td><p>数值，表示允许作为 CmdRectGrayFill 命令的参数的最大灰色填充百分比。</p></td>
<td><p>可选。 如果未指定，则默认值为 100 (百分比) 。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MinGrayFill</strong></p></td>
<td><p>数值，表示允许作为 CmdRectGrayFill 命令的参数的最小灰色填充百分比。</p></td>
<td><p>可选。 如果未指定，则默认值为 1 (百分比) 。</p></td>
</tr>
</tbody>
</table>

 

有关与打印机的矩形区域填充功能关联的命令的信息，请参阅 [矩形区填充命令](rectangle-area-fill-commands.md)。

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




