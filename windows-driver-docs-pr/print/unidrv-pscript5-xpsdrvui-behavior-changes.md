---
title: Unidrv/PScript5 XPSDrv UI 行为更改
description: Unidrv/PScript5 XPSDrv UI 行为更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd7d4dbbfbbc5e2a32aadacac321a83b7cf42630
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786025"
---
# <a name="unidrvpscript5-xpsdrv-ui-behavior-changes"></a>Unidrv/PScript5 XPSDrv UI 行为更改


在 XPSDrv 模式下运行的 Unidrv/PScript5 驱动程序将创建以下核心驱动程序默认 UI 行为更改。 下表中 ("仅 PS" 表示行为更改特定于 PScript5 驱动程序。 "仅 Unidrv" 表示行为更改特定于 Unidrv 驱动程序。 如果这两个短语都未出现，则行为更改适用于 Unidrv 和 PScript5 驱动程序。 ) 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>UI</th>
<th>非 XPSDrv 行为</th>
<th>XPSDrv 行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>方向</p>
<p> (<strong>布局</strong> "选项卡) </p></td>
<td><p>仅 (PS) 硬编码的 UI 具有三个选项：纵向、横向和旋转横向。</p></td>
<td><p>仅) 硬编码方向 UI 未显示时，才 (PS。</p></td>
</tr>
<tr class="even">
<td><p>复制计数</p>
<p> (<strong>高级</strong> "选项卡) </p></td>
<td><p> (Unidrv 仅) 始终显示 "复制计数" UI，除非 GPD 文件具有 "Collate" 功能，其中包含 " <em> ConcealFromUI？： TRUE"：</p>
<p> (Unidrv 仅) 启用 EMF 后，将硬编码的复制计数 UI 设置为具有最大值9999或 GPD 文件指定的 * MaxCopies 值的上限。</p>
<p> (Unidrv 仅在禁用 EMF 后) ，副本计数具有 GPD file * MaxCopies 值的上限。</p>
<p>仅) 复制计数 UI 始终显示时， (PS，其上限为9999。</p></td>
<td><p> (Unidrv 仅) 复制计数 UI 的行为与禁用 EMF 的非 XPSDrv 行为相同。</p>
<p>只有始终显示 (PS) 复制计数，其中上限是在 PPD 文件的 * MSXPSMaxCopies 值中指定的。 如果 PPD 文件未指定 * MSXPSMaxCopies，则上限设置为1。</p></td>
</tr>
<tr class="odd">
<td><p>排序</p>
<p> (<strong>高级</strong> "选项卡) </p></td>
<td><p>启用 EMF 后，逐份打印的 UI (这是将显示为硬编码) 的 "复制计数" 旁边的复选框。</p>
<p>禁用 EMF 后，仅当 GPD 或 PPD 文件将 "Collate" 指定为受支持的功能，并且 "Collate" GPD 或 PPD 功能不受任何设备设置功能的约束时，才会显示逐份打印功能。</p></td>
<td><p>排序的 UI 的行为与禁用 EMF 的非 XPSDrv 行为相同。</p></td>
</tr>
<tr class="even">
<td><p>颜色</p>
<p> (<strong>纸张/质量</strong> "选项卡) </p></td>
<td><p>仅当 GPD ColorMode 功能有一个颜色选项时，才会显示 " (Unidrv 仅) 颜色" 和 "黑白 UI" 选项。</p></td>
<td><p>仅当 GPD ColorMode 功能具有一个颜色选项并且 ColorMode 功能未指定 " </em> ConcealFromUI？： TRUE" 时，才会显示 (Unidrv 仅) 颜色与黑白 UI 选择。</p></td>
</tr>
<tr class="odd">
<td><p>ICM 方法，ICM 意向</p>
<p> (<strong>高级</strong> "选项卡) </p></td>
<td><p>ICM 方法 UI 具有三个用于 Unidrv 的 hard0coded 选项：已禁用、按主机或按驱动程序。 此 UI 有一个硬编码选项，适用于 PScript5 驱动程序的设备。</p>
<p>ICM 意向 UI 具有四个硬编码选项：图形、图片、证明或匹配。</p></td>
<td><p>不显示 oded ICM 方法和 ICM 意向 UI。</p></td>
</tr>
<tr class="even">
<td><p>缩放</p>
<p> (<strong>高级</strong> "选项卡) </p></td>
<td><p>Unidrv 不显示缩放用户界面。</p>
<p>PScript5 驱动程序显示 (1%-1000% ) 的硬编码范围的缩放用户界面。</p></td>
<td><p>不显示硬编码缩放用户界面。 你可以定义一般的 GPD 或 PPD 缩放功能 (这会显示在高级树视图 UI 中) 或者提供自定义缩放用户界面。</p></td>
</tr>
<tr class="odd">
<td><p>TrueType 字体</p>
<p> (<strong>高级</strong> "选项卡) </p></td>
<td><p>硬编码 TrueType 字体 UI 有两个选项： "用设备字体替换" 或 "下载为软字体"。</p></td>
<td><p>不显示硬编码 TrueType 字体 UI。</p></td>
</tr>
<tr class="even">
<td><p>每张纸打印的页数</p>
<p> (<strong>布局</strong> "选项卡) </p></td>
<td><p>对于 Unidrv，如果启用了 EMF，则每个工作表的页面 UI 将显示七个硬编码选项：1、2、4、6、9、16和手册。</p>
<p>对于 PScript5，UI 显示7个硬编码选项：1、2、4、6、9、16和手册。</p></td>
<td><p>不显示每个工作表 UI 的硬编码页面。</p></td>
</tr>
<tr class="odd">
<td><p>其他 EMF 模拟功能</p>
<p> (各种选项卡) </p></td>
<td><p>其他 EMF 模拟功能显示在下列位置：</p>
<ul>
<li>在 "布局" 选项卡中，
<ul>
<li>"基于 Winprint 的 NUp 边界 UI" 复选框</li>
<li>基于 Winprint 的页面顺序 UI，其中包含两个硬编码选项：从前向后和向后。</li>
</ul></li>
<li>在 "高级" 选项卡中：
<ul>
<li>具有两个选项的硬编码 "高级打印功能"： Enabled 或 Disabled。</li>
<li>带有四个选项的基于 Winprint 的 NUp 方向 UI：向右、向下、向下、向左、向下、向下、向左、向下、向左移动。</li>
<li>基于 Winprint 的手册边缘 UI。</li>
</ul></li>
</ul></td>
<td><p>不会显示任何基于硬编码或基于 winprint 的 EMF 模拟功能。</p></td>
</tr>
<tr class="even">
<td><p>通过 Unidrv 呈现功能</p>
<p> (各种选项卡) </p></td>
<td><p> (Unidrv 仅) 呈现功能在两个位置进行硬编码：质量宏 UI ("纸张/质量" 选项卡上) 并在 "高级" 选项卡 (上将文本打印为图形) 。</p></td>
<td><p> (Unidrv 仅) 未显示任何硬编码的 Unidrv 呈现功能。</p></td>
</tr>
<tr class="odd">
<td><p>通过 PScript5 呈现功能</p>
<p> (<strong>高级</strong> "选项卡) </p></td>
<td><p>仅 (PS) 硬编码的 "PostScript 选项" 包括： PostScript 输出选项、TrueType 字体下载选项、PostScript 语言级别、发送 PostScript 错误处理程序、镜像输出和负输出。</p></td>
<td><p>仅 (PS) 未显示任何硬编码 PS 呈现功能。</p></td>
</tr>
<tr class="even">
<td><p>Form-Tray 分配表</p>
<p> (<strong>DeviceSettings</strong> "选项卡) </p></td>
<td><p>将始终显示 "Form-Tray 分配" 表，以使管理员能够选择送送送纸器分配。</p></td>
<td><p>Core Unidrv 或 PScript5 驱动程序不会显示窗体托盘分配表 UI。 可以提供自定义 UI。</p></td>
</tr>
<tr class="odd">
<td><p>字体替换表</p>
<p> (<strong>DeviceSettings</strong> "选项卡) </p></td>
<td><p>字体替换表始终显示，使管理员能够选择 TrueType 字体到设备的字体替换。</p></td>
<td><p>Core Unidrv 或 PScript5 驱动程序未显示字体替换表 UI。 供应商插件可以提供自己的自定义 UI。</p></td>
</tr>
<tr class="even">
<td><p>设备功能（按 Unidrv）</p>
<p> (<strong>DeviceSettings</strong> "选项卡) </p></td>
<td><p> (Unidrv 仅) 硬编码功能 UI 包含</p>
<p>字体盒或外部字体安装程序。</p></td>
<td><p> (Unidrv 仅) 未显示任何硬编码的 Unidrv 设备功能。</p></td>
</tr>
<tr class="odd">
<td><p>设备功能（按 PScript5）</p>
<p> (<strong>DeviceSettings</strong> "选项卡) </p></td>
<td><p>仅 (PS) 硬编码功能 UI 包含：可用的 PostScript 内存、输出协议、在前后发送-D、转换灰色文本、转换灰色图形、添加欧元货币、作业超时、等待超时、要下载为大纲的最小字体大小和下载为位图的最大字体大小。</p></td>
<td><p>仅 (PS) 未显示任何硬编码 PS 设备功能。</p></td>
</tr>
</tbody>
</table>

 

 

 




