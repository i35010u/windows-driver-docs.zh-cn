---
title: 颜色命令
description: 颜色命令
keywords:
- 打印机命令 WDK Unidrv，颜色
- 颜色命令 WDK Unidrv
- 背景颜色选项 WDK Unidrv
- 调色板 WDK Unidrv
- 模式 WDK Unidrv
- 画笔 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0321fbb3f28167236b71388e09292b4bf253aa22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797697"
---
# <a name="color-commands"></a>颜色命令





本主题介绍用于打印的颜色命令，其中包含以下各节：

用于选择主背景色的命令

用于控制打印机调色板的命令

用于选择模式画笔的命令

所有命令都使用 [命令条目格式](command-entry-format.md)指定。

### <a name="commands-for-selecting-primary-background-colors"></a><a href="" id="ddk-commands-for-selecting-primary-background-colors-gg"></a>用于选择主背景色的命令

下表中的 [打印机命令](printer-commands.md) 由不支持可编程调色板的打印机使用，如平面彩色打印机 (例如，点阵打印机) 和某些调色板打印机 (例如，早期的喷墨打印机) 。

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
<td><strong>CmdSelectBlackColor</strong></td>
<td><p>用于选择黑色背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><strong>CmdSelectBlueColor</strong></td>
<td><p>用于选择蓝色背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><strong>CmdSelectCyanColor</strong></td>
<td><p>用于选择背景青色颜色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><strong>CmdSelectGreenColor</strong></td>
<td><p>用于选择绿色背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><strong>CmdSelectMagentaColor</strong></td>
<td><p>用于选择洋红色背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectRedColor</strong></p></td>
<td><p>用于选择红色背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectYellowColor</strong></p></td>
<td><p>用于选择黄色背景色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectWhiteColor</strong></p></td>
<td><p>用于选择背景白颜色的命令。</p></td>
<td><p>可选。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

### <a name="commands-for-controlling-printer-palettes"></a><a href="" id="ddk-commands-for-controlling-printer-palettes-gg"></a>用于控制打印机调色板的命令

下表中的 [打印机命令](printer-commands.md) 用于支持用于前台 (文本和矢量) 打印以及用于光栅打印的可编程调色板的打印机。

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
<td><p><strong>CmdBeginPaletteDef</strong></p></td>
<td><p>用于初始化调色板定义的命令。</p></td>
<td><p>可选。 如果未指定，则不需要初始化调色板定义。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdEndPaletteDef</strong></p></td>
<td><p>用于结束调色板定义的命令。</p></td>
<td><p>可选。 如果未指定，则无需命令即可结束调色板定义。</p>
<p><em>可以指定 Order 属性。 如果不是，则使用与 ColorMode 功能的最近执行的<a href="option-selection-command.md" data-raw-source="[option selection command](option-selection-command.md)">选项选择命令</a>相关联的<strong> </em> Order</strong>属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdBeginPaletteReDef</strong></p></td>
<td><p>用于初始化调色板重定义的命令。</p></td>
<td><p>可选。 如果未指定，则不需要对调色板重新定义进行初始化。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdEndPaletteReDef</strong></p></td>
<td><p>用于结束调色板重定义的命令。</p></td>
<td><p>可选。 如果未指定，则无需命令即可结束调色板重定义。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdDefinePaletteEntry</strong></p></td>
<td><p>用于定义调色板项的命令。</p></td>
<td><p>如果打印机支持调色板，则为必需。</p>
<p>在 24 BPP 模式下，Unidrv 允许 <em> PaletteSize 为1的调色板。 这样，GPD 开发人员便可以为其设备实现直接的 RGB 颜色选择命令。 为此，请将<strong> </em> PaletteSize</strong>设置为1，并在<strong>CmdDefinePaletteEntry</strong>命令中指定 "选择颜色" 命令。 还必须指定 CmdSelectPaletteEntry 命令，但可以将其定义为 <strong>NULL</strong> 命令。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdRedefinePaletteEntry</strong></p></td>
<td><p>用于重新定义调色板项的命令。</p></td>
<td><p>可选。 如果未指定， <strong>CmdDefinePaletteEntry</strong> 将用于重新定义调色板项。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectPaletteEntry</strong></p></td>
<td><p>用于选择调色板项作为当前颜色的命令。</p></td>
<td><p>如果打印机支持调色板，则为必需。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

### <a name="commands-for-selecting-pattern-brushes"></a><a href="" id="ddk-commands-for-selecting-pattern-brushes-gg"></a>用于选择模式画笔的命令

下表中的 [打印机命令](printer-commands.md) 用于支持下载和选择图案画笔的打印机。

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
<td><p><strong>CmdDownloadPattern</strong></p></td>
<td><p>用于将画笔图案传递到打印机的命令。</p></td>
<td><p>可选。 如果已指定，则还必须指定 <strong>CmdSelectPattern</strong> 。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectBlackBrush</strong></p></td>
<td><p>命令为当前画笔形式的实心黑色画笔。</p></td>
<td><p>如果打印机支持画笔，则为必需。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CmdSelectPattern</strong></p></td>
<td><p>用于选择已下载的画笔图案的命令。</p></td>
<td><p>可选。 如果已指定，则还必须指定 <strong>CmdDownloadPattern</strong> 。</p></td>
</tr>
<tr class="even">
<td><p><strong>CmdSelectWhiteBrush</strong></p></td>
<td><p>用于选择作为当前画笔的纯色空白画笔的命令。</p></td>
<td><p>可选。</p></td>
</tr>
</tbody>
</table>

 

 

 




