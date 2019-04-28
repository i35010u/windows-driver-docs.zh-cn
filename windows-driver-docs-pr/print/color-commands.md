---
title: 颜色命令
description: 颜色命令
ms.assetid: 752a3c1d-05f1-4f5e-9ef2-e51721ef7cc4
keywords:
- 打印机命令 WDK Unidrv，颜色
- 颜色命令 WDK Unidrv
- 背景色选项 WDK Unidrv
- 调色板 WDK Unidrv
- WDK Unidrv 模式
- 画笔 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 233234cd9a43ad51d98479ddbe4a7e18e7621eac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351937"
---
# <a name="color-commands"></a>颜色命令





本主题介绍用于打印，颜色命令，它包含以下各节：

用于选择主背景色的命令

用于控制打印机调色板的命令

用于选择模式画笔的命令

使用指定的所有命令[命令条目格式](command-entry-format.md)。

### <a href="" id="ddk-commands-for-selecting-primary-background-colors-gg"></a>用于选择主背景色的命令

[打印机命令](printer-commands.md)下表中不支持可编程的调色板，例如平面彩色打印机 （例如，点阵打印机） 的打印机和使用某些调色板打印机 （例如，早期喷墨打印机打印机）。

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
<td><strong>CmdSelectBlackColor</strong></td>
<td><p>若要选择黑色背景颜色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><strong>CmdSelectBlueColor</strong></td>
<td><p>若要选择蓝色背景颜色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><strong>CmdSelectCyanColor</strong></td>
<td><p>若要选择蓝绿色背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><strong>CmdSelectGreenColor</strong></td>
<td><p>选择绿色背景颜色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><strong>CmdSelectMagentaColor</strong></td>
<td><p>若要选择洋红色背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectRedColor</strong></p></td>
<td><p>若要选择红色背景颜色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectYellowColor</strong></p></td>
<td><p>选择黄色背景颜色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectWhiteColor</strong></p></td>
<td><p>若要选择白色的背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

### <a href="" id="ddk-commands-for-controlling-printer-palettes-gg"></a>用于控制打印机调色板的命令

[打印机命令](printer-commands.md)下表中使用的支持可编程调色板，这两个前景 （文本和矢量） 打印和光栅打印的打印机。

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
<td><p><strong>CmdBeginPaletteDef</strong></p></td>
<td><p>若要初始化的颜色调色板定义的命令。</p></td>
<td><p>可选。 如果未指定，则需要调色板定义未初始化。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdEndPaletteDef</strong></p></td>
<td><p>若要结束的调色板定义的命令。</p></td>
<td><p>可选。 如果未指定，没有命令需要结束调色板定义。</p>
<p><em>可以指定 Order 属性。 如果不是， <strong></em>顺序</strong>与最近执行相关联的属性<a href="option-selection-command.md" data-raw-source="[option selection command](option-selection-command.md)">选项选择命令</a>对于 ColorMode 功能使用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdBeginPaletteReDef</strong></p></td>
<td><p>若要初始化颜色调色板重定义的命令。</p></td>
<td><p>可选。 如果未指定，则需要调色板重新定义未初始化。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdEndPaletteReDef</strong></p></td>
<td><p>若要结束调色板重定义的命令。</p></td>
<td><p>可选。 如果未指定，没有命令需要结束调色板重定义。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdDefinePaletteEntry</strong></p></td>
<td><p>若要定义面板条目的命令。</p></td>
<td><p>所需打印机是否支持调色板。</p>
<p>在 24 BPP 模式下，Unidrv 调色板允许为其<em>PaletteSize 为 1。 这允许 GPD 开发人员实现他们的设备的直接 RGB 颜色选择命令。 若要执行此操作，设置 <strong></em>PaletteSize</strong>为 1，并指定在选择颜色命令<strong>CmdDefinePaletteEntry</strong>命令。 CmdSelectPaletteEntry 命令还必须指定，但可以定义为<strong>NULL</strong>命令。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdRedefinePaletteEntry</strong></p></td>
<td><p>若要重新定义面板条目的命令。</p></td>
<td><p>可选。 如果未指定，否则<strong>CmdDefinePaletteEntry</strong>习惯重新定义的调色板条目。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectPaletteEntry</strong></p></td>
<td><p>若要选择作为当前颜色的调色板条目的命令。</p></td>
<td><p>所需打印机是否支持调色板。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

### <a href="" id="ddk-commands-for-selecting-pattern-brushes-gg"></a>用于选择模式画笔的命令

[打印机命令](printer-commands.md)下表中使用的打印机支持下载和选择模式的画笔。

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
<td><p><strong>CmdDownloadPattern</strong></p></td>
<td><p>若要将非画笔图案传送到打印机的命令。</p></td>
<td><p>可选。 如果指定， <strong>CmdSelectPattern</strong>还必须指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectBlackBrush</strong></p></td>
<td><p>为当前画笔的命令为纯黑色画笔。</p></td>
<td><p>所需打印机是否支持画笔。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectPattern</strong></p></td>
<td><p>若要选择已下载的画笔图案的命令。</p></td>
<td><p>可选。 如果指定， <strong>CmdDownloadPattern</strong>还必须指定。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectWhiteBrush</strong></p></td>
<td><p>若要选择作为当前画笔的纯白色画笔的命令。</p></td>
<td><p>可选。</p></td>
</tr>
</tbody>
</table>

 

 

 




