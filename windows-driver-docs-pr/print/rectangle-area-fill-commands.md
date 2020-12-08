---
title: 矩形区域填充命令
description: 矩形区域填充命令
keywords:
- 矩形区域填充命令 WDK Unidrv
- 填充矩形区域 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63494833b660d8be80e654b9c2ce2d10688f98f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807063"
---
# <a name="rectangle-area-fill-commands"></a>矩形区域填充命令





下表列出了矩形区域填充命令。 所有命令都使用 [命令条目格式](command-entry-format.md)指定。

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
<td><p>CmdRectBlackFill</p></td>
<td><p>用于黑色填充矩形的命令。</p></td>
<td><p>可选。 如果未指定此值，则 Unidrv 将通过指定 CmdRectGrayFill 命令和灰色百分比 * MaxGrayFill 来尝试黑色填充。</p></td>
</tr>
<tr class="even">
<td><p>CmdRectGrayFill</p></td>
<td><p>用于灰色填充矩形的命令。  (不会擦除背景。 ) </p></td>
<td><p>可选。 如果未指定，则 Unidrv 假定没有灰色填充功能。 命令字符串通常包含 GrayPercentage 变量。</p></td>
</tr>
<tr class="odd">
<td><p>CmdRectWhiteFill</p></td>
<td><p>用于填充矩形的命令。  (清除背景。 ) </p></td>
<td><p>可选。 如果未指定，则 Unidrv 假定没有擦除白色填充。 在这种情况下，如果应用程序请求白色填充，Unidrv 将返回失败，因为灰色填充无法擦除背景。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetRectHeight</p></td>
<td><p>用于设置矩形高度的命令。</p></td>
<td><p>可选。 如果指定了 CmdSetRectWidth，则必须指定。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetRectSize</p></td>
<td><p>命令来设置矩形的宽度和高度。</p>
<p>Windows 2000 或更高版本不支持。</p></td>
<td><p>可选。 用于在一个命令中设置宽度和高度的打印机。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetRectWidth</p></td>
<td><p>用于设置矩形宽度的命令。</p></td>
<td><p>可选。 如果指定了 CmdSetRectHeight，则必须指定。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




