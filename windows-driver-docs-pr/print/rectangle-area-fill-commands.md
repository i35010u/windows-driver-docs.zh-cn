---
title: 矩形区域填充命令
description: 矩形区域填充命令
ms.assetid: b9401126-4173-4187-960a-dc5ce69d3522
keywords:
- 矩形区域填充命令 WDK Unidrv
- 填充矩形区域 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21a1ab975584a559681ac350097641ba20b0bdc2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382601"
---
# <a name="rectangle-area-fill-commands"></a>矩形区域填充命令





下表列出了的矩形区域填充命令。 使用指定的所有命令[命令条目格式](command-entry-format.md)。

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
<td><p>CmdRectBlackFill</p></td>
<td><p>命令为黑色填充矩形。</p></td>
<td><p>可选。 如果未指定，Unidrv 将尝试通过使用灰色的百分比指定 CmdRectGrayFill 命令黑色填充 * MaxGrayFill。</p></td>
</tr>
<tr class="even">
<td><p>CmdRectGrayFill</p></td>
<td><p>命令为灰色填充矩形。 （不清除后台）。</p></td>
<td><p>可选。 如果未指定，Unidrv 假定没有任何灰色填充功能。 命令字符串通常包含 GrayPercentage 变量。</p></td>
</tr>
<tr class="odd">
<td><p>CmdRectWhiteFill</p></td>
<td><p>命令为白色填充矩形。 （清除后台）。</p></td>
<td><p>可选。 如果未指定，Unidrv 假定没有擦除白色填充。 Unidrv 的情况下，如果应用程序将返回失败请求白色填充，因为灰色填充无法擦除背景。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetRectHeight</p></td>
<td><p>若要设置的矩形高度的命令。</p></td>
<td><p>可选。 如果指定 CmdSetRectWidth 指定必须。</p></td>
</tr>
<tr class="odd">
<td><p>CmdSetRectSize</p></td>
<td><p>若要设置矩形的宽度和高度的命令。</p>
<p>不支持适用于 Windows 2000 或更高版本。</p></td>
<td><p>可选。 用于在一个命令中设置的宽度和高度的打印机。</p></td>
</tr>
<tr class="even">
<td><p>CmdSetRectWidth</p></td>
<td><p>若要设置矩形宽度的命令。</p></td>
<td><p>可选。 如果指定 CmdSetRectHeight 指定必须。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




