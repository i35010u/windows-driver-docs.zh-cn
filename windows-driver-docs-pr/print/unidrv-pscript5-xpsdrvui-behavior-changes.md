---
title: Unidrv/PScript5 XPSDrv UI 行为更改
description: Unidrv/PScript5 XPSDrv UI 行为更改
ms.assetid: 7c594f40-8e75-4c8b-a60e-42f74116c75f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1395d36098f6eeab848fde8b80ff1aaf13a91b0f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346533"
---
# <a name="unidrvpscript5-xpsdrv-ui-behavior-changes"></a>Unidrv/PScript5 XPSDrv UI 行为更改


在 XPSDrv 模式下运行的 Unidrv/PScript5 驱动程序将创建以下核心驱动程序的默认 UI 行为更改。 （在下表中，"仅 PS"方法的行为更改为特定于 PScript5 驱动程序。 "仅 Unidrv"平均值的行为更改是特定于 Unidrv 驱动程序。 如果未显示这两个这些短语，行为更改适用于 Unidrv 和 PScript5 驱动程序。）

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
<td><p>Orientation</p>
<p>(<strong>布局</strong>选项卡)</p></td>
<td><p>(仅 PS)硬编码的 UI 有三个选项：纵向、 横向和旋转的横向。</p></td>
<td><p>(仅 PS)硬编码的方向 UI 不会显示。</p></td>
</tr>
<tr class="even">
<td><p>份数</p>
<p>(<strong>高级</strong>选项卡)</p></td>
<td><p>(仅 Unidrv)副本计数 UI 会始终显示，除非 GPD 文件具有与"逐份打印"功能"<em>ConcealFromUI？:TRUE":</p>
<p>(仅 Unidrv)当启用 EMF、 副本计数 UI 是硬编码为具有的上限为 9999 的最大值或指定 GPD 文件的 * MaxCopies 值。</p>
<p>(仅 Unidrv)副本计数时 EMF 处于禁用状态，具有 GPD 文件的上限 * MaxCopies 值。</p>
<p>(仅 PS)副本计数将始终显示 UI，上限硬编码为 9999。</p></td>
<td><p>(仅 Unidrv)副本计数 UI 的行为与 EMF 已禁用的非 XPSDrv 行为相同。</p>
<p>(仅 PS)始终显示为副本计数，带有 PPD 文件中指定的上限 * MSXPSMaxCopies 值。 如果未指定 PPD 文件的上限设置为 1 * MSXPSMaxCopies。</p></td>
</tr>
<tr class="odd">
<td><p>逐份打印</p>
<p>(<strong>高级</strong>选项卡)</p></td>
<td><p>启用 EMF 后，逐份打印用户界面 （这是副本计数旁的复选框） 是硬编码来显示。</p>
<p>禁用 EMF，GPD 或 PPD 文件指定为受支持的功能，"逐份打印"和"逐份打印"GPD 或 PPD 功能不受任何设备设置功能时，才会显示逐份打印。</p></td>
<td><p>逐份打印用户界面的行为与 EMF 已禁用的非 XPSDrv 行为相同。</p></td>
</tr>
<tr class="even">
<td><p>颜色</p>
<p>(<strong>纸张/质量</strong>选项卡)</p></td>
<td><p>(仅 Unidrv)如果 GPD ColorMode 功能具有一种颜色选择显示的颜色与白色和黑色 UI 选择。</p></td>
<td><p>(仅 Unidrv)GPD ColorMode 功能具有一种颜色选择并且未指定 ColorMode 功能之后，显示与黑色或白色 UI 选择颜色"</em>ConcealFromUI？:TRUE"。</p></td>
</tr>
<tr class="odd">
<td><p>ICM 方法，ICM 含义</p>
<p>(<strong>高级</strong>选项卡)</p></td>
<td><p>ICM 方法 UI 有三个用于 Unidrv hard0coded 选项： 已禁用，由主机，或由驱动程序。 此 UI 具有一个硬编码选项 PScript5 设备的驱动程序。</p>
<p>ICM 意向 UI 具有硬编码的四个选项：图形、 图片、 概念验证或匹配项。</p></td>
<td><p>不会显示硬 oded ICM 方法和 ICM 意向 UI。</p></td>
</tr>
<tr class="even">
<td><p>缩放</p>
<p>(<strong>高级</strong>选项卡)</p></td>
<td><p>Unidrv 不显示缩放用户界面。</p>
<p>PScript5 驱动程序显示了具有硬编码的范围 （%1%-1000年） 的缩放 UI。</p></td>
<td><p>硬编码的缩放 UI 不会显示。 可以定义的泛型 GPD 或 PPD 缩放功能 （这高级的树视图用户界面中所示），或者提供自定义缩放用户界面。</p></td>
</tr>
<tr class="odd">
<td><p>TrueType 字体</p>
<p>(<strong>高级</strong>选项卡)</p></td>
<td><p>硬编码的 TrueType 字体 UI 具有两个选项：用设备字体或下载为软字体替换。</p></td>
<td><p>硬编码的 TrueType 字体 UI 不会显示。</p></td>
</tr>
<tr class="even">
<td><p>每张纸打印的页</p>
<p>(<strong>布局</strong>选项卡)</p></td>
<td><p>对于 Unidrv，启用 EMF 后，表 UI 每页显示七个硬编码选项：1、 2、 4、 6、 9、 16 和手册。</p>
<p>对于 PScript5，UI 显示七个硬编码选项：1、 2、 4、 6、 9、 16 和手册。</p></td>
<td><p>每个表硬编码页 UI 不会显示。</p></td>
</tr>
<tr class="odd">
<td><p>其他 EMF 模拟功能</p>
<p>（各个选项卡）</p></td>
<td><p>在以下位置中显示其他 EMF 模拟功能：</p>
<ul>
<li>在布局选项卡
<ul>
<li>Winprint 基于 NUp 边框 UI 复选框</li>
<li>基于 Winprint 的页顺序的用户界面使用硬编码的两个选项：前端到后并返回到前面。</li>
</ul></li>
<li>在高级选项卡：
<ul>
<li>硬编码"高级打印功能"的两个选项：启用或禁用。</li>
<li>Winprint 基于 NUp 方向 UI 包含四个选项：向右依次向下、 向单击右下方，然后左侧取、 向单击左下方。</li>
<li>Winprint 基于手册边缘 UI。</li>
</ul></li>
</ul></td>
<td><p>硬编码或基于 winprint 的 EMF 模拟功能都不会显示。</p></td>
</tr>
<tr class="even">
<td><p>呈现按 Unidrv 的功能</p>
<p>（各个选项卡）</p></td>
<td><p>(仅 Unidrv)呈现功能在两个位置是硬编码：（在纸张/质量选项卡） 的质量宏 UI 和打印文本作为图形 （的高级选项卡）。</p></td>
<td><p>(仅 Unidrv)硬编码 Unidrv 呈现功能都不会显示。</p></td>
</tr>
<tr class="odd">
<td><p>呈现按 PScript5 的功能</p>
<p>(<strong>高级</strong>选项卡)</p></td>
<td><p>(仅 PS)硬编码"PostScript 选项"包括：PostScript 输出选项，TrueType 字体下载选项，PostScript 语言级别发送 PostScript 错误处理程序、 镜像的输出和负数的输出。</p></td>
<td><p>(仅 PS)硬编码 PS 呈现功能都不会显示。</p></td>
</tr>
<tr class="even">
<td><p>窗体的送纸器分配表</p>
<p>(<strong>DeviceSettings</strong>选项卡)</p></td>
<td><p>窗体的送纸器分配表始终显示若要使管理员能够选择的送纸器格式分配。</p></td>
<td><p>核心 Unidrv 或 PScript5 驱动程序不显示窗体的送纸器分配表 UI。 你可以提供自定义 UI。</p></td>
</tr>
<tr class="odd">
<td><p>字体替换表</p>
<p>(<strong>DeviceSettings</strong>选项卡)</p></td>
<td><p>字体替换表将始终显示，以使管理员能够选择 TrueType 字体设备字体替换。</p></td>
<td><p>核心 Unidrv 或 PScript5 驱动程序不显示字体替换表 UI。 供应商插件可以提供其自己的自定义 UI。</p></td>
</tr>
<tr class="even">
<td><p>通过 Unidrv 设备功能</p>
<p>(<strong>DeviceSettings</strong>选项卡)</p></td>
<td><p>(仅 Unidrv)硬编码功能 UI 包括</p>
<p>字体盒或外部字体安装程序。</p></td>
<td><p>(仅 Unidrv)硬编码 Unidrv 设备功能都不会显示。</p></td>
</tr>
<tr class="odd">
<td><p>通过 PScript5 设备功能</p>
<p>(<strong>DeviceSettings</strong>选项卡)</p></td>
<td><p>(仅 PS)硬编码功能 UI 包括：可用的 PostScript 内存、 输出协议发送 CTRL-D 前/后、 转换灰色文本，将纯灰度图形转换，当作位图下载添加欧元货币、 作业超时、 等待超时、 当作轮廓，下载的最小字体大小和最大字体大小。</p></td>
<td><p>(仅 PS)硬编码 PS 设备功能都不会显示。</p></td>
</tr>
</tbody>
</table>

 

 

 




