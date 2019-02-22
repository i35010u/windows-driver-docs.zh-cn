---
title: Unidrv/PScript5 驱动程序默认值 DEVMODE 的安装程序的行为更改
description: Unidrv/PScript5 驱动程序默认值 DEVMODE 的安装程序的行为更改
ms.assetid: 9760d527-0205-477b-bc16-d6aa65b1eaf7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea91b2c247f40713a937bcf35958bef0ad55b6df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519854"
---
# <a name="unidrvpscript5-driver-default-devmode-setup-behavior-changes"></a>Unidrv/PScript5 驱动程序默认值 DEVMODE 的安装程序的行为更改


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
<td><p>(仅 Unidrv)仅设置 DM_ORIENTATION 标志<strong>dmFields</strong>如果 GPD 文件支持&quot;方向&quot;gpd 分析功能。 <strong>dmOrientation</strong>设置为根据&quot;方向&quot;GPD 功能&#39;s GPD 文件中指定的默认选项。</p>
<p>(仅 PS)仅设置 DM_ORIENTATION 标志<strong>dmFields</strong>如果 PPD 文件支持具有的功能&quot;PageOrientation&quot;打印架构关键字。</p>
<p><strong>dmOrientation</strong>设置为<strong>DMORIENT_LANDSCAPE</strong>如果该功能已使用默认选项&quot;横向&quot;或&quot;ReverseLandscape&quot;打印架构关键字。 否则为<strong>dmOrientation</strong>设置为<strong>DMORIENT_PORTRAIT</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_SCALE</p></td>
<td><p>(仅 Unidrv)硬编码为永远不会在中设置 DM_SCALE 标志<strong>dmFields</strong>。</p>
<p>(仅 PS)硬编码为始终设置 DM_SCALE 标志<strong>dmFields</strong>。</p></td>
<td><p>仅设置 DM_SCALE 标志<strong>dmFields</strong>如果 GPD 或 PPD 支持具有的功能&quot;PageScaling&quot;打印架构关键字。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_TTOPTION</p>
<p><strong>dmTTOption</strong></p></td>
<td><p>硬编码来始终在 dmFields，设置 DM_TTOPTION 标志并设置 dmTTOption = DMTT_SUBDEV。</p></td>
<td><p>如果 GPD 或 PPD 支持具有的功能&quot;PageDeviceFontSubstitution&quot;打印架构关键字和功能已使用默认选项&quot;上&quot;打印架构关键字，设置 DM_TTOPTION 标志并将设置<strong>dmTTOption</strong> = <strong>DMTT_SUBDEV</strong>。</p>
<p>否则为如果 GPD 或 PPD 支持具有的功能&quot;PageTrueTypeFontMode&quot;打印架构关键字和以下项之一：</p>
<ul>
<li><p>如果该功能已具有的默认选项&quot;DownloadAsOutlineFont&quot;打印架构关键字，然后设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong> = <strong>DMTT_DOWNLOAD_OUTLINE</strong>.</p></li>
<li><p>如果该功能已具有的默认选项&quot;RenderAsBitmap&quot;打印架构关键字，然后设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong> = <strong>DMTT_BITMAP</strong>;</p></li>
<li><p>如果该功能已具有的默认选项&quot;自动&quot;， &quot;DownloadAsRasterFont&quot;，或&quot;DownloadAsNativeTrueTypeFont&quot;打印架构关键字，然后设置 DM_TTOPTION 标志并设置<strong>dmTTOption</strong> = <strong>DMTT_DOWNLOAD</strong>。</p></li>
</ul>
<p>否则，将在清除 DM_TTOPTION 标志<strong>dmFields</strong>因为打印机并不表示它支持 TrueType 字体替换或下载。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_NUP</p></td>
<td><p>硬编码为始终设置 DM_NUP 标志<strong>dmFields</strong>。</p></td>
<td><p>仅设置 DM_NUP 标志<strong>dmFields</strong>如果 GPD 或 PPD 支持具有的功能&quot;JobNUpAllDocumentsContiguously 或&quot;DocumentNUp&quot;打印架构关键字。</p></td>
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
<td><p>仅设置 DM_PRINTQUALITY 和 DM_YRESOLUTION 标志<strong>dmFields</strong>如果 GPD 或 PPD 支持&quot;解析&quot;GPD 或 PPD 功能。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_COLLATE</p>
<p><strong>dmCollate</strong></p></td>
<td><p>硬编码为始终设置 DM_COLLATE 标志<strong>dmFields</strong>，并设置<strong>dmCollate</strong> = DMCOLLATE_TRUE。</p></td>
<td><p>仅设置 DM_COLLATE 标志<strong>dmFields</strong>如果 GPD 或 PPD 支持&quot;逐份打印&quot;GPD 或 PPD 功能。 <strong>dmCollate</strong>设置为根据&quot;Collate&quot; GPD 或 PPD 功能&#39;s GPD 或 PPD.中指定的默认选项</p></td>
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

 

 

 




