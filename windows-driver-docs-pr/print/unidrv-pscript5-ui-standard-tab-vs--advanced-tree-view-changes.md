---
title: Unidrv/PScript5 UI 标准选项卡与高级树视图更改
description: Unidrv/PScript5 UI 标准选项卡与
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f867fe38ec04f01d65bca1326c9c035f8dd2a913
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813503"
---
# <a name="unidrvpscript5-ui-standard-tab-vs-advanced-tree-view-changes"></a>Unidrv/PScript5 UI 标准选项卡与高级树视图更改


以下公共打印架构功能受 UniDrive/PScript5 用户界面 (UI) 支持：

JobPageOrder

仅限 PageOrientation (PS) 

PageDeviceFontSubstitution

PageOutputQuality

JobNUpAllDocumentsContiguously 或 DocumentNUp

如果有自定义的 GPD 或 PPD 功能，或者通过使用 GPD 的 **PrintSchemaKeywordMap** 关键字或 Ppd 的 **MSPrintSchemaKeywordMap** 关键字映射到前面的打印架构功能及其标准打印架构选项的选项，Unidrv/PScript5 驱动程序 UI 以与在非 XPSDrv 模式下运行的 Unidrv 或 PScript5 驱动程序显示的相同方式显示标准选项卡中的功能，除非 GPD 文件中的功能 " \* ConcealFromUI"。 设置为 "TRUE"。

如果从 GPD 或 PPD 自定义功能) 映射的这些打印架构功能 (将显示在 Unidrv/Pscript5 驱动程序 UI 标准选项卡中，而不是显示在 " **高级** " 树视图 UI 的 "打印机功能" 组中，则会显示 COMPSTUI 的标准显示名称和图标。 将忽略这些功能在 GPD 或 PPD 文件中指定的任何显示名称或图标。

若要为这些标准打印功能提供一致的 Unidrv/PScript5 驱动程序 UI，在 XPSDrv 模式下运行的 Unidrv/PScript5 驱动程序具有以下行为。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>打印架构映射功能</th>
<th>XPSDrv 行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>JobPageOrder</p></td>
<td><p>如果 GPD 或 PPD 文件使用 "JobPageOrder" 打印架构关键字定义了一项功能，并且该功能包含具有 "Standard" 和 "Reverse" 打印架构关键字的两个选项，则该功能将显示在 "标准<strong>布局</strong>" 选项卡的 "<strong>页面顺序</strong>" 区域中。否则，GPD 或 PPD 功能将显示在 "<strong>高级</strong>" 树视图 UI 的 "打印机功能" 组中。</p>
<p>当在 "标准<strong>布局</strong>" 选项卡的 "<strong>页面顺序</strong>" 区域中显示该功能时，将出现以下情况：</p>
<ul>
<li><p>如果驱动程序的 GPD 文件未指定 " <em> OutputOrderReversed？： TRUE" 或其 PPD 文件未指定 "DefaultOutputOrder： Reverse"，则 GPD/ppd "Standard" 选项将显示为 "前端到后端 ui" 选项，并且 GPD/ppd "反向" 选项将显示为 "返回到前面的 ui" 选项。</p></li>
<li><p>如果驱动程序的 GPD 文件指定了 " </em> OutputOrderReversed？： TRUE" 或其 PPD 文件指定了 "DefaultOutputOrder： Reverse"，则 GPD/ppd "Standard" 选项将显示为 "返回前端 ui" 选项，并且 GPD/ppd "反向" 选项将显示为 "前端到后端 ui" 选项。</p></li>
</ul>
<p>下面的屏幕截图显示 "打印首选项" 对话框中的 "页面顺序" 区域。</p>
<img src="images/xpsdrv-printingpreferences1.png" alt="Screen shot of the Page Order area on the Printing Preferences dialog box" /></td>
</tr>
<tr class="even">
<td><p>PageOrientation</p>
<p>仅 (PS) </p></td>
<td><p>如果 PPD 定义了具有 "PageOrientation" 打印架构关键字的功能，并且该功能具有 "纵向"、"横向" 和 "ReversePortrait" 打印架构关键字的三个选项，或者使用 "纵向" 和 "横向" 打印架构关键字的两个选项，则该功能将显示在 "标准<strong>布局</strong>" 选项卡的 "<strong>方向</strong>" 区域中。</p>
<p>否则，在 " <strong>高级" 树视图</strong> UI 的 "打印机功能" 组中显示 PPD 功能。</p>
<p>以下屏幕截图显示了 "打印首选项" 对话框中的方向区域。</p>
<img src="images/xpsdrv-printingpreferences2.png" alt="Screen shot of the Orientation area on the Printing Preferences dialog box" />
<p>以下屏幕截图说明了 "打印首选项" 对话框中没有 "旋转横向" 选项) 的方向区 (。</p>
<img src="images/xpsdrv-printingpreferences3.png" alt="Screen shot of the Orientation area (without the Rotated Landscape option) on the Printing Preferences dialog box" /></td>
</tr>
<tr class="odd">
<td><p>PageDeviceFont-Substitution</p></td>
<td><p>如果 GPD 或 PPD 使用 "PageDeviceFontSubstitution" 打印架构关键字定义了一项功能，并且该功能包含包含 "On" 和 "Off" 的两个选项，则在 "<strong>高级</strong>" 选项卡的 "图形" 组中的<strong>TrueType 字体</strong>列表中显示该功能。 "打开" 选项显示为替换为 <strong>设备字体</strong>，而 "Off" 选项显示为 " <strong>下载为软字体</strong>"。</p>
<p>否则，GPD 或 PPD 功能将显示在 " <strong>高级" 树视图</strong> UI 的 "打印机功能" 组中。</p>
<p>下面的 "高级选项" 对话框屏幕截图显示了 "用设备字体替换" 选项。</p>
<img src="images/xpsdrv-printingpreferences4.png" alt="Screen shot of the Advanced Options dialog box with Substitute with Device font selected" /></td>
</tr>
<tr class="even">
<td><p>PageOutput-Quality</p></td>
<td><p>如果 GPD 或 PPD 使用 "PageOutputQuality" 打印架构关键字定义了一个功能，并且该功能具有 "草稿"、"Normal" 和 "High" 打印架构关键字的三个选项，则该功能将显示在 "标准<strong>纸张/质量</strong>" 选项卡的 "<strong>质量设置</strong>" 区域中。"草稿" 选项显示为<strong>草稿</strong>选项，"Normal" 选项显示为<strong>更好</strong>的选项，"高" 选项显示为<strong>最佳</strong>选项。</p>
<p>否则，GPD 或 PPD 功能将显示在 " <strong>高级" 树视图</strong> UI 的 "打印机功能" 组中。</p>
<p>"打印首选项" 对话框的以下屏幕截图 lustrates "质量设置" 区域。</p>
<img src="images/xpsdrv-printingpreferences5.png" alt="Screen shot of the Quality Settings area on the Printing Preferences dialog box" /></td>
</tr>
<tr class="odd">
<td><p>JobNUpAllDocumentsContiguously 或 DocumentNUp</p></td>
<td><p>如果 GPD 或 PPD 使用 "JobNUpAllDocumentsContiguously" 或 "DocumentNUp" 打印架构关键字定义了一项功能 (仅当不) 存在 "JobNUpAllDocumentsContiguously" 功能时才使用 "DocumentNUp" 功能，并且该功能正好包含六个选项，其中 GPD 或 PPD 关键字名称为数字字符串 (也就是说 "1"、"2"、"4"、"6"、"9" 和 "16" ) 中，功能显示在 "标准<strong>布局</strong>" 选项卡的 "<strong>每张纸的页</strong>" 列表中。</p>
<p>否则，GPD 或 PPD 功能将显示在 " <strong>高级" 树视图</strong> UI 的 "打印机功能" 组中。</p>
<img src="images/xpsdrv-printingpreferences6.png" alt="Screen shot of the Pages per Sheet option on the Printing Preferences dialog box" /></td>
</tr>
</tbody>
</table>

 

对于任何其他自定义 GPD 或 PPD 功能，无论它们是否映射到公共打印架构功能，它们都将始终显示在 " **高级" 树视图** UI 的 "打印机功能" 组中。

 

 




