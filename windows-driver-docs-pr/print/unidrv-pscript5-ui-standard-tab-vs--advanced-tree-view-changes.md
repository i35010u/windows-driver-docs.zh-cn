---
title: Unidrv/PScript5 UI 标准选项卡与高级树视图更改
description: Unidrv/PScript5 UI 标准选项卡与
ms.assetid: 07374e07-f0ca-4e97-8e5f-e5fe54d14af4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab8047427c0a4ac56ea048916b22f694d280941
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464029"
---
# <a name="unidrvpscript5-ui-standard-tab-vs-advanced-tree-view-changes"></a>Unidrv/PScript5 UI 标准选项卡与高级树视图更改


UniDrive/PScript5 用户界面 (UI) 支持以下公共打印架构功能：

JobPageOrder

PageOrientation (仅 PS)

PageDeviceFontSubstitution

PageOutputQuality

JobNUpAllDocumentsContiguously 或 DocumentNUp

如果有自定义 GPD 或 PPD 功能或映射到先前的打印架构功能的选项和其标准的打印架构选项通过使用 GPD 的**PrintSchemaKeywordMap**关键字或 PPD 的**MSPrintSchemaKeywordMap**关键字，Unidrv/PScript5 驱动程序用户界面显示的功能标准选项卡中同样除非 GPD 文件中的功能"Unidrv或PScript5非XPSDrv模式下运行的驱动程序中的显示\*ConcealFromUI？" 设置为"TRUE"。

Unidrv/Pscript5 驱动程序 UI 标准选项卡中，而不是泛型的"打印机功能"组中时显示这些打印架构功能 （它们将映射从 GPD 或 PPD 自定义功能）**高级**树视图 UI，标准显示的显示名称和 COMPSTUI 的图标。 任何显示名称或为这些功能将被忽略 GPD 或 PPD 文件中指定的图标。

若要展示这些标准的打印功能一致 Unidrv/PScript5 驱动 UI，在 XPSDrv 模式下运行的 Unidrv/PScript5 驱动程序具有以下行为。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>打印架构映射的功能</th>
<th>XPSDrv 行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>JobPageOrder</p></td>
<td><p>如果 GPD 或 PPD 文件定义"JobPageOrder"Print Schema 关键字，具有的功能和功能有两个选项的"标准"和"反向"打印架构的关键字，则该功能所示<strong>页序</strong>中的区域标准<strong>布局</strong>选项卡。否则，GPD 或 PPD 功能中的泛型"打印机功能"组中所示<strong>高级</strong>树视图 UI。</p>
<p>当该功能所示<strong>页序</strong>标准中的区域<strong>布局</strong>选项卡上，则满足以下条件：</p>
<ul>
<li><p>如果驱动程序的 GPD 文件未指定"<em>OutputOrderReversed？:TRUE"或其 PPD 文件未指定"DefaultOutputOrder:反向"，然后 GPD/PPD"标准"选项显示为到返回 UI 的选项，前端和 GPD/PPD"反向"选项显示为在回复到前端 UI 选项。</p></li>
<li><p>如果未指定驱动程序的 GPD 文件"</em>OutputOrderReversed？:TRUE"或其 PPD 文件未指定"DefaultOutputOrder:反向"，然后 GPD/PPD"标准"选项显示为在回复到前端 UI 选项和 GPD/PPD"反向"选项显示为从前到回 UI 选项。</p></li>
</ul>
<p>下面的屏幕截图显示打印首选项对话框上的页序区域。</p>
<img src="images/xpsdrv-printingpreferences1.png" alt="Screen shot of the Page Order area on the Printing Preferences dialog box" /></td>
</tr>
<tr class="even">
<td><p>PageOrientation</p>
<p>(仅 PS)</p></td>
<td><p>如果 PPD 定义具有"PageOrientation"打印架构关键字的特征和功能已通过"纵向"、"横向"和"ReversePortrait"打印架构关键字正好有三个选项，或者两个选项与"纵向"和"横向"打印架构关键字，该功能将显示在<strong>方向</strong>标准中的区域<strong>布局</strong>选项卡。</p>
<p>否则，PPD 功能中的泛型"打印机功能"组中所示<strong>高级树视图</strong>UI。</p>
<p>下面的屏幕截图显示打印首选项对话框上的方向区域。</p>
<img src="images/xpsdrv-printingpreferences2.png" alt="Screen shot of the Orientation area on the Printing Preferences dialog box" />
<p>下面的屏幕截图演示了在打印首选项对话框中方向区域 （而不会旋转横向选项）。</p>
<img src="images/xpsdrv-printingpreferences3.png" alt="Screen shot of the Orientation area (without the Rotated Landscape option) on the Printing Preferences dialog box" /></td>
</tr>
<tr class="odd">
<td><p>PageDeviceFont-Substitution</p></td>
<td><p>如果 GPD 或 PPD 定义具有"PageDeviceFontSubstitution"打印架构关键字的特征和功能有两个选项的"开"和"关闭"功能的打印架构关键字所示<strong>TrueType 字体</strong>中的列表<strong>高级</strong>选项卡的"图形"组。 "On"选项显示为<strong>用设备字体替换</strong>，并显示为"关闭"选项<strong>下载为软字体</strong>。</p>
<p>否则，GPD 或 PPD 功能中的泛型"打印机功能"组中所示<strong>高级树视图</strong>UI。</p>
<p>高级选项对话框中的以下屏幕截图显示使用所选的设备字体选项替换。</p>
<img src="images/xpsdrv-printingpreferences4.png" alt="Screen shot of the Advanced Options dialog box with Substitute with Device font selected" /></td>
</tr>
<tr class="even">
<td><p>PageOutput-Quality</p></td>
<td><p>如果 GPD 或 PPD 定义具有"PageOutputQuality"打印架构关键字的特征和功能有三个选项使用"草稿"、"Normal"和"高"打印架构关键字，该功能会显示在<strong>质量设置</strong>标准中的区域<strong>纸张/质量</strong>选项卡。"草稿"选项显示为<strong>草稿</strong>选项，"Normal"选项显示为<strong>更好地</strong>选项和"高级"选项显示为<strong>最佳</strong>选项。</p>
<p>否则，GPD 或 PPD 功能中的泛型"打印机功能"组中所示<strong>高级树视图</strong>UI。</p>
<p>打印首选项对话框中的以下屏幕截图 lustrates 质量设置区域。</p>
<img src="images/xpsdrv-printingpreferences5.png" alt="Screen shot of the Quality Settings area on the Printing Preferences dialog box" /></td>
</tr>
<tr class="odd">
<td><p>JobNUpAllDocumentsContiguously 或 DocumentNUp</p></td>
<td><p>如果 GPD 或 PPD 定义具有"JobNUpAllDocumentsContiguously"或"DocumentNUp"打印架构关键字 （仅当没有"JobNUpAllDocumentsContiguously"的功能存在，将使用"DocumentNUp"功能） 的特征和功能具有完全六个选项的 GPD 或PPD 关键字名称 （即，"1"、"2"、"4"、"6"、"9"和"16"） 的数字字符串，该功能所示<strong>每页</strong>标准中的列表<strong>布局</strong>选项卡。</p>
<p>否则，GPD 或 PPD 功能中的泛型"打印机功能"组中所示<strong>高级树视图</strong>UI。</p>
<img src="images/xpsdrv-printingpreferences6.png" alt="Screen shot of the Pages per Sheet option on the Printing Preferences dialog box" /></td>
</tr>
</tbody>
</table>

 

任何其他自定义 GPD 或 PPD 功能，而不管它们将映射到公共打印架构功能，或不是，如果它们将始终显示，泛型"打印机功能"组中**高级树视图**UI。

 

 




