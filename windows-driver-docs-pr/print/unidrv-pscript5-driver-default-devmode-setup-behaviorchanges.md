---
title: Unidrv/PScript5 驱动程序的默认 DEVMODE 设置行为更改
description: Unidrv/PScript5 驱动程序的默认 DEVMODE 设置行为更改
ms.assetid: 9760d527-0205-477b-bc16-d6aa65b1eaf7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41780d5fd3b6640f209e476b7ba31d3cb55324e8
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464279"
---
# <a name="unidrvpscript5-driver-default-devmode-setup-behavior-changes"></a>Unidrv/PScript5 驱动程序的默认 DEVMODE 设置行为更改


在 XPSDrv 模式下运行的 Unidrv/PScript5 驱动程序创建以下驱动程序默认值 DEVMODE 的安装程序的行为更改。

（在下表中，"仅 PS"方法的行为更改为特定于 PScript5 驱动程序。 "仅 Unidrv"平均值的行为更改是特定于 Unidrv 驱动程序。 如果未显示这两个这些短语，行为更改适用于 Unidrv 和 PScript5 驱动程序。）

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>受影响的默认值 DEVMODE 字段</th>
<th>非 XPSDrv 行为</th>
<th>XPSDrv 行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_ORIENTATION</p>
<p><strong>dmOrientation</strong></p></td>
<td><p>硬编码为始终设置 DM_ORIENTATION 标志<strong>dmFields</strong>，并设置<strong>dmOrientation</strong> = DMORIENT_PORTRAIT。</p></td>
<td><p>(仅 Unidrv)仅设置 DM_ORIENTATION 标志<strong>dmFields</strong> GPD 文件是否支持"方向"gpd 分析功能。 <strong>dmOrientation</strong>集基于"方向"GPD GPD 文件中指定的功能的默认选项。</p>
<p>(仅 PS)仅设置 DM_ORIENTATION 标志<strong>dmFields</strong>如果 PPD 文件支持具有"PageOrientation"打印架构关键字的功能。</p>
<p><strong>dmOrientation</strong>设置为<strong>DMORIENT_LANDSCAPE</strong>该功能是否使用"横向"或"ReverseLandscape"打印架构关键字的默认选项。 否则为<strong>dmOrientation</strong>设置为<strong>DMORIENT_PORTRAIT</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_SCALE</p></td>
<td><p>(仅 Unidrv)硬编码为永远不会在中设置 DM_SCALE 标志<strong>dmFields</strong>。</p>
<p>(仅 PS)硬编码为始终设置 DM_SCALE 标志<strong>dmFields</strong>。</p></td>
<td><p>仅设置 DM_SCALE 标志<strong>dmFields</strong>如果 GPD 或 PPD 支持具有"PageScaling"打印架构关键字的功能。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_TTOPTION</p>
<p><strong>dmTTOption</strong></p></td>
<td><p>硬编码来始终在 dmFields，设置 DM_TTOPTION 标志并设置 dmTTOption = DMTT_SUBDEV。</p></td>
<td><p>如果 GPD 或 PPD 支持具有"PageDeviceFontSubstitution"打印架构关键字的特征和功能有"开"打印架构关键字默认选项，设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong>  =  <strong>DMTT_SUBDEV</strong>。</p>
<p>否则，如果 GPD 或 PPD 支持具有"PageTrueTypeFontMode"的功能打印架构关键字和下列选项之一：</p>
<ul>
<li><p>如果该功能已具有"DownloadAsOutlineFont"打印架构关键字的默认选项，然后设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong> = <strong>DMTT_DOWNLOAD_OUTLINE</strong>。</p></li>
<li><p>如果该功能已具有"RenderAsBitmap"打印架构关键字的默认选项，然后设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong> = <strong>DMTT_BITMAP</strong>;</p></li>
<li><p>如果该功能具有一个默认选项，使用"自动"、"DownloadAsRasterFont"或"DownloadAsNativeTrueTypeFont"打印架构的关键字，然后设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong> = <strong>DMTT_下载</strong>。</p></li>
</ul>
<p>否则，将在清除 DM_TTOPTION 标志<strong>dmFields</strong>因为打印机并不表示它支持 TrueType 字体替换或下载。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_NUP</p></td>
<td><p>硬编码为始终设置 DM_NUP 标志<strong>dmFields</strong>。</p></td>
<td><p>仅设置 DM_NUP 标志<strong>dmFields</strong> GPD 或 PPD 支持一项功能与"JobNUpAllDocumentsContiguously 或"DocumentNUp"打印架构关键字。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_COLOR</p></td>
<td><p>硬编码为始终设置 DM_COLOR 标志<strong>dmFields</strong>。</p></td>
<td><p>仅设置 DM_COLOR 标志<strong>dmFields</strong>如果 GPD 或 PPD 指定打印机是彩色打印机。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_PRINTQUALITY DM_YRESOLUTION</p></td>
<td><p>(仅 Unidrv)硬编码为始终设置 DM_PRINTQUALITY 标志<strong>dmFields</strong>。</p>
<p>(仅 PS)硬编码为始终设置 DM_PRINTQUALITY 和 DM_YRESOLUTION 标志<strong>dmFields</strong>。</p></td>
<td><p>仅设置 DM_PRINTQUALITY 和 DM_YRESOLUTION 标志<strong>dmFields</strong>如果 GPD 或 PPD 支持"解析"GPD 或 PPD 功能。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_COLLATE</p>
<p><strong>dmCollate</strong></p></td>
<td><p>硬编码为始终设置 DM_COLLATE 标志<strong>dmFields</strong>，并设置<strong>dmCollate</strong> = DMCOLLATE_TRUE。</p></td>
<td><p>仅设置 DM_COLLATE 标志<strong>dmFields</strong>如果 GPD 或 PPD 支持"逐份打印"GPD 或 PPD 功能。 <strong>dmCollate</strong>基于的"逐份打印"GPD 或 GPD 或 PPD.中指定的 PPD 功能的默认选项集</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_ICMMETHOD DM_ICMINTENT</p></td>
<td><p>(仅 Unidrv)硬编码为始终设置 DM_ICMMETHOD 和 DM_ICMINTENT 标志<strong>dmFields</strong>。</p>
<p>(仅 PS)如果 PPD 指定打印机是彩色打印机，设置 DM_ICMMETHOD 和 DM_ICMINTENT 标志<strong>dmFields</strong>。</p></td>
<td><p>永远不会设置的 DM_ICMMETHOD 或 DM_ICMINTENT 标志<strong>dmFields</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_DITHERTYPE</p></td>
<td><p>(仅 Unidrv)硬编码为始终设置 DM_DITHERTYPE 标志<strong>dmFields</strong>。</p></td>
<td><p>(仅 Unidrv)永远不会在中设置 DM_DITHERTYPE 标志<strong>dmFields</strong>。</p></td>
</tr>
</tbody>
</table>

 

 

 




